pipeline {
    agent any

    stages {

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