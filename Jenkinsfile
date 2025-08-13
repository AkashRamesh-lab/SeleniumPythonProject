pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
        REPORT_NAME = 'report.html'
    }

    stages {
        stage('Setup Python') {
            steps {
                echo 'Setting up virtual environment and installing dependencies...'
                bat """
                    python -m venv %VENV_DIR%
                    call %VENV_DIR%\\Scripts\\activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                """
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests and generating HTML report...'
                bat """
                    call %VENV_DIR%\\Scripts\\activate
                    pytest tests/ --html=%REPORT_NAME%
                """
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
