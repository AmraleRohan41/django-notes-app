pipeline {
    agent any

    environment {
        IMAGE_NAME = "amralerohan41/notes-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AmraleRohan41/django-notes-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:latest .
                '''
            }
        }

        stage('Verify Image') {
            steps {
                sh '''
                docker images | grep notes-app
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f notes-app || true

                docker run -d \
                  --name notes-app \
                  -p 8000:8000 \
                  $IMAGE_NAME:latest
                '''
            }
        }
    }
}