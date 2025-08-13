pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
        REPORT_NAME = 'report.html'
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
                // Git repo is automatically cloned if Jenkinsfile is from SCM
            }
        }

        stage('Setup Python') {
            steps {
                echo 'Setting up virtual environment and installing dependencies...'
                sh '''
                    python3 -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests and generating HTML report...'
                sh '''
                    . ${VENV_DIR}/bin/activate
                    pytest tests/ --html=${REPORT_NAME}
                '''
            }
        }

        stage('Publish HTML Report') {
            steps {
                echo 'Publishing HTML report...'
                publishHTML (target: [
                    reportName: 'Test Report',
                    reportDir: '.',
                    reportFiles: "${REPORT_NAME}",
                    keepAll: true,
                    alwaysLinkToLastBuild: true,
                    allowMissing: false
                ])
            }
        }
    }
}
