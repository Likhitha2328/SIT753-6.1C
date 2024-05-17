pipeline {
    agent any
    environment {
        RECIPIENT_EMAIL = 'itsmyemail1228@gmail.com'
    }
    triggers {
        pollSCM('H/5 * * * *') // Poll the Git repository every 5 minutes
    }
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code using Maven...'
                    // Actual command: sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit tests using JUnit and integration tests...'
                    // Actual command: sh 'mvn test'
                }
            }
            post {
                always {
                    script {
                        echo 'Sending notification email for Unit and Integration Tests stage...'
                        emailext (
                            to: "${itsmyemail1228@gmail.com}",
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
                    // Actual command: sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan using OWASP Dependency-Check...'
                    // Actual command: sh 'mvn dependency-check:check'
                }
            }
            post {
                always {
                    script {
                        echo 'Sending notification email for Security Scan stage...'
                        emailext (
                            to: "${itsmyemail1228@gmail.com}",
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
                    // Actual command: sh 'scp target/my-app.war user@staging-server:/path/to/deploy'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment...'
                    // Actual command: sh 'mvn verify -Pstaging'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production server...'
                    // Actual command: sh 'scp target/my-app.war user@production-server:/path/to/deploy'
                }
            }
        }
    }
    post {
        always {
            script {
                echo 'Sending notification email for the overall pipeline status...'
                emailext (
                    to: "${itsmyemail1228@gmail.com}",
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
