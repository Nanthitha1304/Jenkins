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
        bat '''
        python -m venv venv
        venv\\Scripts\\activate
        pip install -r requirements.txt
        '''
    }
}

        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest > test_report.txt'  // Runs tests and saves results in test_report.txt
            }
        }
        stage('Run Flask App') {
            steps {
                sh '. venv/bin/activate && nohup python -m flask run --host=0.0.0.0 --port=8000 &'
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
