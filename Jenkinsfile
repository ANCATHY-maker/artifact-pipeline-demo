pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching source code'
                checkout scm
            }
        }

        stage('Code Quality Check!') {
            steps {
                echo 'Checking code quality'
                bat '''
                findstr GOOD quality.txt > nul
                if errorlevel 1 (
                    echo Code Quality Failed
                    exit 1
                ) else (
                    echo Code Quality Passed
                )
                '''
            }
        }

        stage('Generate Report') {
            steps {
                echo 'Generating report'
                bat 'echo Report generated > report.txt'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '*.txt', fingerprint: true
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed - code blocked'
        }
        success {
            echo 'Pipeline completed successfully'
        }
    }
}
