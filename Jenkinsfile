pipeline {
    agent any
    environment {
        PYTHON = '/usr/bin/python3'  // Make sure to adjust if necessary
        PIP = '/usr/bin/pip3'        // Ensure pip3 is installed
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Ensure you have the correct repository and branch
                    git branch: 'main', url: 'https://github.com/Nanthitha1304/Jenkins.git'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure pip is installed and dependencies are installed using pip3
                    sh 'which python3'   // Verify python3 path
                    sh 'which pip3'      // Verify pip3 path
                    sh 'pip3 install -r requirements.txt'  // Use pip3 for installation
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Run the tests and capture the output in the test_report.txt file
                    sh 'pytest > test_report.txt'
                }
            }
        }
        stage('Run Flask App') {
            steps {
                script {
                    // Run Flask app in the background, no need for `nohup`
                    sh 'python3 -m flask run --host=0.0.0.0 --port=8000 &'
                }
            }
        }
        stage('Open in Browser') {
            steps {
                script {
                    // Opening a browser on Jenkins server might not be possible.
                    // Commenting it for now as Jenkins does not have a graphical interface
                    echo 'Flask App is running on http://localhost:8000'
                    // If you want to open it on a local machine, run it outside of Jenkins
                    // Example for local testing:
                    // if (isUnix()) {
                    //     sh 'xdg-open http://localhost:8000'
                    // } else {
                    //     bat 'start http://localhost:8000'
                    // }
                }
            }
        }
    }
    post {
        always {
            // Archive test results regardless of the pipeline status
            archiveArtifacts artifacts: 'test_report.txt', allowEmptyArchive: true
            echo 'Pipeline completed.'
        }
    }
}
