pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'pytest'
            }
        }
    }
}
