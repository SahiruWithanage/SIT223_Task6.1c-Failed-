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
                success {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Unit and Integration Tests - ${currentBuild.result}",
                             body: "The Unit and Integration Tests stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
                    }
                }
                failure {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Unit and Integration Tests - ${currentBuild.result}",
                             body: "The Unit and Integration Tests stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
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
                success {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Security Scan - ${currentBuild.result}",
                             body: "The Security Scan stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
                    }
                }
                failure {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Security Scan - ${currentBuild.result}",
                             body: "The Security Scan stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
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
                success {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Integration Tests on Staging - ${currentBuild.result}",
                             body: "The Integration Tests on Staging stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
                    }
                }
                failure {
                    script {
                        def logFiles = findFiles(glob: '**/*.log')
                        def logContent = logFiles.collect { readFile(it.path) }.join('\n\n')
                        mail to: 'hesh.zsg@gmail.com',
                             subject: "Integration Tests on Staging - ${currentBuild.result}",
                             body: "The Integration Tests on Staging stage has ${currentBuild.result}. Here are the logs:\n\n${logContent}"
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
