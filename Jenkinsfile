pipeline {
    agent any
    environment {
        LOG_FILE = 'pipeline.log'  // Define the log file to store all output
    }
    stages {
        stage('Build') {
            steps {
                // Start capturing build output and append to the log file
                script {
                    sh 'echo "Starting Build Stage" | tee -a $LOG_FILE'
                    sh 'echo "Building the code..." | tee -a $LOG_FILE'
                    // Your build command here
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                // Capture unit and integration test output
                script {
                    sh 'echo "Starting Unit and Integration Tests Stage" | tee -a $LOG_FILE'
                    sh 'echo "Running unit and integration tests..." | tee -a $LOG_FILE'
                    // Your testing command here
                }
            }
            post {
                always {
                    script {
                        // Send email with the captured log file so far
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                            body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '$LOG_FILE'
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                // Continue capturing output for code analysis
                script {
                    sh 'echo "Starting Code Analysis Stage" | tee -a $LOG_FILE'
                    sh 'echo "Analyzing the code..." | tee -a $LOG_FILE'
                    // Your code analysis command here
                }
            }
        }
        stage('Security Scan') {
            steps {
                // Capture security scan output
                script {
                    sh 'echo "Starting Security Scan Stage" | tee -a $LOG_FILE'
                    sh 'echo "Performing security scan..." | tee -a $LOG_FILE'
                    // Your security scan command here
                }
            }
            post {
                always {
                    script {
                        // Send email with the updated log file
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Security Scan - ${currentBuild.currentResult}",
                            body: "The Security Scan stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '$LOG_FILE'
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Continue capturing output for deploy to staging
                script {
                    sh 'echo "Starting Deploy to Staging Stage" | tee -a $LOG_FILE'
                    sh 'echo "Deploying to staging..." | tee -a $LOG_FILE'
                    // Your deployment command here
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                // Capture integration tests on staging output
                script {
                    sh 'echo "Starting Integration Tests on Staging Stage" | tee -a $LOG_FILE'
                    sh 'echo "Running integration tests on staging..." | tee -a $LOG_FILE'
                    // Your staging test command here
                }
            }
            post {
                always {
                    script {
                        // Send email with the updated log file
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Integration Tests on Staging - ${currentBuild.currentResult}",
                            body: "The Integration Tests on Staging stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '$LOG_FILE'
                        )
                    }
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                // Continue capturing output for deploy to production
                script {
                    sh 'echo "Starting Deploy to Production Stage" | tee -a $LOG_FILE'
                    sh 'echo "Deploying to production..." | tee -a $LOG_FILE'
                    // Your production deployment command here
                }
            }
        }
    }
    post {
        always {
            script {
                // Final email with the complete log file after all stages are done
                emailext(
                    to: 'hesh.zsg@gmail.com',
                    subject: "Final Pipeline Log - ${currentBuild.currentResult}",
                    body: "The entire pipeline has completed. Please find the final attached log.",
                    attachmentsPattern: '$LOG_FILE'
                )
            }
        }
    }
}
