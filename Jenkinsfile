pipeline {
    agent any
    
    stages {
        stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'maheshwali', url: 'https://github.com/maheshwali/Task-6.1C.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Task: Build the code using Maven
                // Maven commands or build scripts can be added here
            }
        }
stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                // Task: Run unit tests
                // Commands to execute unit tests can be added here
                
                echo 'Running integration tests...'
                // Task: Run integration tests
                // Commands to execute integration tests can be added here
            }
            post {
                success {
                    emailext attachLog: true,
                    body: 'Unit and integration tests passed.',
                    subject: 'Test Success',
                    to: 'wali.walimahesh16@gmail.com'
                }
                failure {
                    emailext attachLog: true,
                    body: 'Unit and integration tests failed.',
                    subject: 'Test Failure',
                    to: 'wali.walimahesh16@gmail.com'
                }
            }
   }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code using SonarQube...'
                // Task: Integrate a code analysis tool (e.g., SonarQube)
                // Commands to trigger code analysis with SonarQube can be added here
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Task: Perform a security scan on the code (e.g., SonarQube Security Plugin)
                // Commands to trigger security scan can be added here
            }
            post {
                success {
                    emailext attachLog: true,
                    body: 'Security scan passed',
                    subject: 'Security Scan Success',
                    to: 'wali.walimahesh16@gmail.com'
                }
                failure {
                    emailext attachLog: true,
                    body: 'Security vulnerabilities found',
                    subject: 'Security Scan Failure',
                    to: 'wali.walimahesh16@gmail.com'
                }
            }
  }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to staging server...'
                // Task: Deploy the application to a staging server (e.g., AWS EC2 instance)
                // Commands to deploy to staging server can be added here
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                // Task: Run integration tests on the staging environment
                // Commands to execute integration tests on staging can be added here
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production server...'
                // Task: Deploy the application to a production server (e.g., AWS EC2 instance)
                // Commands to deploy to production server can be added here
            }
        }
    }
}

    

            
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit tests using JUnit and integration tests...'
                }
            }
            post {
                always {
                    script {
                        echo 'Sending notification email for Unit and Integration Tests stage...'
                        emailext (
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Pipeline - Unit and Integration Tests: ${currentBuild.currentResult}",
                            body: """Stage: Unit and Integration Tests
                            Result: ${currentBuild.currentResult}
                            See attached logs for details.""",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code using SonarQube...'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan using OWASP Dependency-Check...'
                }
            }
            post {
                always {
                    script {
                        echo 'Sending notification email for Security Scan stage...'
                        emailext (
                            to: "${RECIPIENT_EMAIL}",
                            subject: "Jenkins Pipeline - Security Scan: ${currentBuild.currentResult}",
                            body: """Stage: Security Scan
                            Result: ${currentBuild.currentResult}
                            See attached logs for details.""",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging server...'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment...'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production server...'
                }
            }
        }
    }
    post {
        always {
            script {
                echo 'Sending notification email for the overall pipeline status...'
                emailext (
                    to: "${RECIPIENT_EMAIL}",
                    subject: "Jenkins Pipeline - Overall Status: ${currentBuild.currentResult}",
                    body: """Pipeline: ${env.JOB_NAME}
                    Build: #${env.BUILD_NUMBER}
                    Result: ${currentBuild.currentResult}
                    See attached logs for details.""",
                    attachLog: true
                )
            }
        }
    }
}
