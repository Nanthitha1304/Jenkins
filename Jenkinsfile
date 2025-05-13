pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 --version || sudo apt-get install python3 -y
                    pip3 --version || sudo apt-get install python3-pip -y
                    pip3 install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest > test_report.txt' 
            }
        }
        stage('Run Flask App') {
            steps {
                sh 'nohup python3 -m flask run --host=0.0.0.0 --port=8000 &'
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
