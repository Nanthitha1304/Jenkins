pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nanthitha1304/Jenkins.git'
            }
        }
       stage('Install Dependencies') {
    stage('Install Dependencies') {
    steps {
        script {
            if (isUnix()) {
                sh 'install_dependencies.sh'  // Shell command for Unix
            } else {
                bat 'install_dependencies.bat'  // Batch command for Windows
            }
        }
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
