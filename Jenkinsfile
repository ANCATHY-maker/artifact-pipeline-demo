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
                findstr GOOD quality.txt >nul
                IF %ERRORLEVEL% NEQ 0 (
                    echo Code quality check FAILED
                    exit /b 1
                ) ELSE (
                    echo Code quality check PASSED
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
