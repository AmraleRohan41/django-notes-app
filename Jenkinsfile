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
                --network notes-network \
                -p 8001:8000 \
                -e DB_NAME=test_db \
                -e DB_USER=root \
                -e DB_PASSWORD=root \
                -e DB_HOST=db_cont \
                -e DB_PORT=3306 \
                amralerohan41/notes-app:latest

                sleep 10

                docker exec notes-app python manage.py migrate
                '''
            }
        }
    }
}