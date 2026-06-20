pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AmraleRohan41/django-notes-app.git'
            }
        }

        stage('Verify Repository') {
            steps {
                sh '''
                pwd
                ls -la
                '''
            }
        }

        stage('Verify Kubernetes Files') {
            steps {
                sh '''
                ls -la k8s
                '''
            }
        }

        stage('Verify Dockerfile') {
            steps {
                sh '''
                cat Dockerfile
                '''
            }
        }
    }
}