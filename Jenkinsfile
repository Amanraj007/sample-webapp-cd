pipeline {
    agent any

    environment {
        DOCKER_HUB = 'your-dockerhub-username'
        APP_NAME = 'sample-webapp'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Amanraj007/sample-webapp-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_HUB/$APP_NAME:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push $DOCKER_HUB/$APP_NAME:latest"
                }
            }
        }
    }
}

