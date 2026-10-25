
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace'
            }
        }

        stage('Build') {
            steps {
                bat 'if not exist output mkdir output'
                bat 'echo Build completed > output\\build.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'if exist output\\build.txt (exit /b 0) else (exit /b 1)'
                echo 'Basic test passed'
            }
        }

        stage('Package') {
            steps {
                powershell 'Compress-Archive -Path output -DestinationPath application-artifact.zip -Force'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'application-artifact.zip'
        }
    }
}
