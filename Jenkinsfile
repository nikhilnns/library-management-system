pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Python Version') {
            steps {
                bat "\"C:\\Users\\user\\AppData\\Local\\Programs\\Python\\Python313\\python.exe\" --version"
            }
        }

        stage('Upgrade Pip') {
            steps {
                bat "\"C:\\Users\\user\\AppData\\Local\\Programs\\Python\\Python313\\python.exe\" -m pip install --upgrade pip"
            }
        }

        stage('Install Requirements') {
            steps {
                bat "\"C:\\Users\\user\\AppData\\Local\\Programs\\Python\\Python313\\python.exe\" -m pip install -r requirements.txt"
            }
        }

        stage('Docker Version') {
            steps {
                bat "docker --version"
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t library-app ."
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat 'docker rm -f library-ms-app || exit 0'
                    bat 'docker run -d --name library-ms-app -p 5002:5000 library-app'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed successfully'
        }
    }
}