pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'TestingEnv'
        PRODUCTION_ENVIRONMENT = 'YourNameProduction'
        }
        stages {
            stage('Build') {
                steps {
                    echo "Fetching the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                    echo "Compiling the code and generating necessary artifacts"
                }
            }
            stage('Test') {
                steps {
                    echo "Running unit tests"
                    echo "Running integration tests"
                }
            }
            stage('Code Quality Check') {
                steps {
                    echo "Checking the quality of the code"
                }
            }
            stage('Deploy') {
                steps {
                    echo "Deploying the application to the testing environment: ${env.TESTING_ENVIRONMENT}"
                }
            }
            stage('Approval') {
                steps {
                    echo "Waiting for approval..."
                    sleep time: 10, unit: 'SECONDS'
                }
            }
            stage('Deploy to Production') {
                steps {
                    echo "Deploying the application to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
                }
            }
        }
    }
