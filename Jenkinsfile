pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/Dashboard/SIT753-6.1C'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'production'
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                script {
                    echo "Waiting for manual approval..."
                    sleep 10 // simulate a manual approval process
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            emailext (
                to: 'itsmyemail1228@gmail.com',
                subject: "Pipeline Success: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: """The pipeline has completed successfully.
                         Job: ${env.JOB_NAME}
                         Build Number: ${env.BUILD_NUMBER}
                         
                         See details at: ${env.BUILD_URL}"""
            )
        }
        failure {
            emailext (
                to: 'itsmyemail1228@gmail.com',
                subject: "Pipeline Failure: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: """The pipeline has failed.
                         Job: ${env.JOB_NAME}
                         Build Number: ${env.BUILD_NUMBER}
                         
                         See details at: ${env.BUILD_URL}"""
            )
        }
    }
}
