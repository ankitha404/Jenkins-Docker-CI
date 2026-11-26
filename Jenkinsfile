pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "abh-app"
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                bat 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe app.py'
            }
        }

        stage('3. Docker Verification') {
            steps {
                bat 'where docker'
                bat 'docker --version'
                bat 'docker ps'
            }
        }

        stage('4. Build & Tag Docker Image') {
            steps {
                bat "docker build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('5. Push Image to Registry') {
            steps {
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded!"
        }
    }
}
