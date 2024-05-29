pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'itsmyemail1228@gmail.com' // Update this with your email
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the project using Maven...'
                    // Example build tool: Maven
                    // sh 'mvn clean install'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit tests and integration tests using JUnit and Selenium...'
                    // Example test tools: JUnit for unit tests, Selenium for integration tests
                    // sh 'mvn test'
                }
            }
            post {
                always {
                    script {
                        emailext (
                            subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                            body: "The Unit and Integration Tests stage has finished with status: ${currentBuild.currentResult}. Please check the attached logs for more details.",
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis using SonarQube...'
                    // Example code analysis tool: SonarQube
                    // sh 'sonar-scanner'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan using OWASP ZAP...'
                    // Example security scan tool: OWASP ZAP
                    // sh 'zap-cli start && zap-cli scan'
                }
            }
            post {
                always {
                    script {
                        emailext (
                            subject: "Security Scan: ${currentBuild.currentResult}",
                            body: "The Security Scan stage has finished with status: ${currentBuild.currentResult}. Please check the attached logs for more details.",
                            to: "${env.EMAIL_RECIPIENTS}",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying application to staging environment on AWS EC2...'
                    // Example deployment tool: AWS CLI for EC2 deployment
                    // sh 'aws deploy create-deployment ...'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests in staging environment using Selenium...'
                    // Example integration test tool: Selenium
                    // sh 'selenium test ...'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying application to production environment on AWS EC2...'
                    // Example deployment tool: AWS CLI for EC2 deployment
                    // sh 'aws deploy create-deployment ...'
                }
            }
        }
    }

    post {
        always {
            script {
                emailext (
                    subject: "Pipeline: ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                    body: "The pipeline has finished with status: ${currentBuild.currentResult}. Please check the attached logs for more details.",
                    to: "${env.EMAIL_RECIPIENTS}",
                    attachLog: true
                )
            }
        }
    }
}
