pipeline {
    agent any

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
                docker build -t notes-app:latest .
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
    }
}