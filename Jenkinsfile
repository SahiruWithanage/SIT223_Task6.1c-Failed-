pipeline {
    agent any

    environment {
        LOG_FILE = 'pipeline.log'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'echo "Starting Build Stage" | tee -a $LOG_FILE'
                    sh 'echo "Building the code..." | tee -a $LOG_FILE'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    sh 'echo "Starting Unit and Integration Tests Stage" | tee -a $LOG_FILE'
                    sh 'echo "Running unit and integration tests..." | tee -a $LOG_FILE'
                }
            }
            post {
                always {
                    script {
                        // Ensure the log file is available before sending email
                        archiveArtifacts artifacts: '$LOG_FILE', allowEmptyArchive: true

                        // Retry sending email if it fails
                        try {
                            emailext(
                                to: 'hesh.zsg@gmail.com',
                                subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                                body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Please find the attached logs.",
                                attachmentsPattern: '$LOG_FILE'
                            )
                        } catch (Exception e) {
                            echo "Email sending failed: ${e.message}. Retrying..."
                            sleep 10
                            emailext(
                                to: 'hesh.zsg@gmail.com',
                                subject: "Retry: Unit and Integration Tests - ${currentBuild.currentResult}",
                                body: "Retrying to send logs after failure. The Unit and Integration Tests stage has ${currentBuild.currentResult}. Please find the attached logs.",
                                attachmentsPattern: '$LOG_FILE'
                            )
                        }
                    }
                }
            }
        }
        // Add more stages here as needed
    }
}
