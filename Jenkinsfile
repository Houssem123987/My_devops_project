pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "houssem128/myapp:1.0"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Houssem123987/My_devops_project.git'
            }
        }

        stage('Build Docker') {
            steps {
                bat "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        stage('Push Docker') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                                   bat """
                                   echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                                   docker push %IMAGE_NAME%:latest
                                   docker logout
                                   """
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
