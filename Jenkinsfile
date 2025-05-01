pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-creds')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mohsin6837/mynodecicd.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("mohsin955/node-app")
                }
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        def app = docker.build("mohsin955/node-app")
                        app.push('latest')
                    }
                }
            }
        }
    }
}

