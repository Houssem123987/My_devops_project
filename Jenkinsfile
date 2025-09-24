pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "houssem128/myapp:1.0"
        DOCKERHUB_CREDENTIALS = credential('houssem128-dockerhub')
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
                bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                bat 'docker push houssem128/myapp:latest'
            }
         }
      }
}
