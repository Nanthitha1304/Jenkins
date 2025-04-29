pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Building the application..."'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'pytest tests/'   // Example if Python
            }
        }
        stage('Report') {
            steps {
                echo 'Tests completed!'
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

