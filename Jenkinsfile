pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = "amralerohan41"
        IMAGE_NAME = "notes-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:latest .
                '''
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Tag Image') {
            steps {
                sh '''
                docker tag $IMAGE_NAME:latest $DOCKERHUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push $DOCKERHUB_USERNAME/$IMAGE_NAME:latest
                '''
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop notes-app || true
                docker rm notes-app || true

                docker run -d \
                --name notes-app \
                -p 8000:8000 \
                amralerohan41/notes-app:latest
                '''
            }
        }
    }
}