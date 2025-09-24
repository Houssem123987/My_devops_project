pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "houssem128/myapp:1.0"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Houssem123987/My_devops_project.git'
            }
        }

        stage('Build Docker') {
            steps {
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Push Docker') {
    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                      usernameVariable: 'DOCKER_USER', 
                                      passwordVariable: 'DOCKER_PASS')]) {
        bat """
        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
        docker push houssem128/myapp:1.0
        docker logout
        """
    }
}
        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
