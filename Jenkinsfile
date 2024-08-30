pipeline {
    agent any

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Task: Compile and package the code using Maven
                // Tool: Maven
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit...'
                // Task: Run unit tests and integration tests to ensure code correctness and integration
                // Tool: JUnit, TestNG
            }
            post {
                always {
                    script {
                        def result = currentBuild.currentResult
                        echo "Test stage completed with result: ${result}"
                        echo "Sending email notification..."

                        def logOutput = sh(script: 'tail -n 100 $WORKSPACE/target/surefire-reports/*.txt', returnStdout: true).trim()

                        try {
                            sh """
                                echo "Test stage completed with result: ${result}.\n\nLogs:\n${logOutput}" | mailx -s "Test Stage: ${result}" nikhilnaga2@gmail.com
                            """
                            echo "Email sent successfully."
                        } catch (Exception e) {
                            echo "Failed to send email: ${e.getMessage()}"
                        }
                    }
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                // Task: Analyze the code for quality, adherence to coding standards, and potential issues
                // Tool: SonarQube
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency-Check...'
                // Task: Scan the code for known vulnerabilities in dependencies
                // Tool: OWASP Dependency-Check
            }
            post {
                always {
                    script {
                        def result = currentBuild.currentResult
                        echo "Security scan stage completed with result: ${result}"
                        echo "Sending email notification..."

                        def logOutput = sh(script: 'tail -n 100 $WORKSPACE/owasp-report/*.txt', returnStdout: true).trim()

                        try {
                            sh """
                                echo "Security scan stage completed with result: ${result}.\n\nLogs:\n${logOutput}" | mailx -s "Security Scan Stage: ${result}" nikhilnaga2@gmail.com
                            """
                            echo "Email sent successfully."
                        } catch (Exception e) {
                            echo "Failed to send email: ${e.getMessage()}"
                        }
                    }
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
                echo 'Running integration tests on the staging environment...'
                // Task: Run integration tests in the staging environment to ensure production-like behavior
                // Tool: Selenium, Postman
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to the production environment...'
                // Task: Deploy the application to a production server (e.g., AWS EC2 instance)
                // Tool: AWS CLI, Ansible
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
