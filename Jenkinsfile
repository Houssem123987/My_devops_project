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

        stage('Push vers Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'houssem128-dockerhub',
                                                 usernameVariable: 'DOCKER_USER',
                                                 passwordVariable: 'DOCKER_PASS')]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                    bat "docker push %DOCKER_IMAGE%"
                }
            }
        }
    }
}
