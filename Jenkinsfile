pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t exp8-cicd:latest .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker images exp8-cicd:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop exp8-app || true'
                sh 'docker rm exp8-app || true'
                sh 'docker run -d --name exp8-app -p 8081:80 exp8-cicd:latest'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed.'
        }
    }
}