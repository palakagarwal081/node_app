pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'palak081/node-app'
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds'  // Jenkins credentials ID
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                git 'https://github.com/palakagarwal081/node_app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully!'
        }
        failure {
            echo 'Something went wrong!'
        }
    }
}
