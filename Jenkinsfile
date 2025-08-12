pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'pytest --junitxml=test-results/results.xml'
            }
        }
    }

    post {
        always {
            junit 'test-results/results.xml'
        }
    }
}
