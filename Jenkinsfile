pipeline {
    agent {
        docker {
            image 'python:3.10' // Use the latest stable Python version
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt' 
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest > test_report.txt' 
            }
        }
        stage('Run Flask App') {
            steps {
                sh 'nohup python -m flask run --host=0.0.0.0 --port=8000 &'
            }
        }
        stage('Open in Browser') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'xdg-open http://localhost:8000'
                    } else {
                        bat 'start http://localhost:8000'
                    }
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'test_report.txt', allowEmptyArchive: true
            echo 'Pipeline completed.'
        }
    }
}
