pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Capturing the build output to a log file
                script {
                    sh 'echo "Building the code..." | tee build.log'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                // Capturing the test output to a log file
                script {
                    sh 'echo "Running unit and integration tests..." | tee test.log'
                }
            }
            post {
                always {
                    script {
                        // Archive the log files so they can be attached
                        archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true

                        // Attach the logs to the email
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Unit and Integration Tests - ${currentBuild.currentResult}",
                            body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '**/*.log'
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                // Capturing the code analysis output to a log file
                script {
                    sh 'echo "Analyzing the code..." | tee analysis.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                // Capturing the security scan output to a log file
                script {
                    sh 'echo "Performing security scan..." | tee security.log'
                }
            }
            post {
                always {
                    script {
                        // Archive the log files so they can be attached
                        archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true

                        // Attach the logs to the email
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Security Scan - ${currentBuild.currentResult}",
                            body: "The Security Scan stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '**/*.log'
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Capturing the deploy output to a log file
                script {
                    sh 'echo "Deploying to staging..." | tee deploy.log'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                // Capturing the staging integration test output to a log file
                script {
                    sh 'echo "Running integration tests on staging..." | tee staging_tests.log'
                }
            }
            post {
                always {
                    script {
                        // Archive the log files so they can be attached
                        archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true

                        // Attach the logs to the email
                        emailext(
                            to: 'hesh.zsg@gmail.com',
                            subject: "Integration Tests on Staging - ${currentBuild.currentResult}",
                            body: "The Integration Tests on Staging stage has ${currentBuild.currentResult}. Please find the attached logs.",
                            attachmentsPattern: '**/*.log'
                        )
                    }
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                // Capturing the production deploy output to a log file
                script {
                    sh 'echo "Deploying to production..." | tee production_deploy.log'
                }
            }
        }
    }
}
