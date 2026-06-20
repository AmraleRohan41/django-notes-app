pipeline {
    agent any

    stages {

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