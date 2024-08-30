pipeline {
    agent any

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the code using automation tool Maven...'
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests to ensure code correctness and integration by using tool JUnit'
            }
            post{
                success{
                    emailext attachLog: true, body: 'This stage is success', subject: 'The Unit and intergration stage of $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
                }
                failure{
                    emailext attachLog: true, body: 'This stage is Failure', subject: 'The Unit and intergration stage of $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyze the code for quality using SonarQube'
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'perform a security scan on the code using a tool using OWASP for any vulnerabilities...'
            }
            post{
                success{
                    emailext attachLog: true, body: 'This stage is success', subject: 'Security Scan stage of $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
                }
                failure{
                    emailext attachLog: true, body: 'This stage is Failure', subject: 'Security Scan stage of $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
                }
            }
        }
        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to the staging environment...'
                // Task: Deploy the application to a staging server (e.g., AWS EC2 instance)
                // Tool: AWS CLI, Ansible
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment using Selenim...'
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production environment using AWS EC2...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
