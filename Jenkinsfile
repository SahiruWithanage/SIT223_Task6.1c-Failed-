lpipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build the code using a build automation tool like Maven or Gradle to compile and package your code.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Run unit tests using a framework like JUnit or TestNG, and integration tests to ensure the different components work together.'
            }
            post {
                always{
                        emailext  (
                        
                        
                        attachLog: true,
                    body: "The Security Scan stage has successfully completed.",
                        subject: "Security Scan",
                    to: 'hesh.zsg@gmail.com')
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyze the code using a tool like SonarQube to ensure it meets industry standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Perform a security scan using a tool like OWASP ZAP or Snyk to identify any vulnerabilities.'
            }
            post {
                success {
                    mail to: 'hesh.zsg@gmail.com',
                    subject: "Security Scan",
                    body: "The Security Scan stage has successfully completed."
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploy the application to a staging server, such as an AWS EC2 instance.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on the staging environment using tools like Apache JMeter or Eggplant to ensure the application functions as expected in a production-like environment.'
            }
            post {
                success {
                    mail to: 'hesh.zsg@gmail.com',
                    subject: "Integration Tests on Staging",
                    body: "The Integration Tests on Staging has successfully completed."
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploy the application to a production server, such as an AWS EC2 instance.'
            }
        }
    }
}
