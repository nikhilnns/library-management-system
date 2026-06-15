pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Version') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t library-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f library-ms-app || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name library-ms-app -p 5002:5000 library-app'
            }
        }
    }
}