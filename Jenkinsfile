pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
<<<<<<< HEAD
                sh 'pip install -r requirements.txt' 
=======
                sh 'pip install -r requirements.txt'
>>>>>>> d10d6e11673bc04f5f435a8562822b0a1888e692
            }
        }
        stage('Run Tests') {
            steps {
<<<<<<< HEAD
                sh 'pytest > test_report.txt'  // Runs tests and saves results in test_report.txt
=======
                sh 'pytest > test_report.txt'  // Generates a test report
>>>>>>> d10d6e11673bc04f5f435a8562822b0a1888e692
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



