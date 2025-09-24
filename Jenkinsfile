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
        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
