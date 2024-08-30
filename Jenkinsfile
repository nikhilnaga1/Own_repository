pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Use Maven to build the code
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Run unit tests with JUnit
                sh 'mvn test'
                // Run integration tests (assuming a profile for integration tests)
                sh 'mvn verify -P integration-tests'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                    mail to: 'nikhilnaga2@gmail.com',
                         subject: "Unit and Integration Test Results: ${currentBuild.currentResult}",
                         body: "The tests have completed with status: ${currentBuild.currentResult}. Please check the attached test results.",
                         attachLog: true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Run SonarQube analysis
                withSonarQubeEnv('SonarQube') { // Assuming SonarQube is configured in Jenkins
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Run OWASP Dependency Check or Snyk
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
            post {
                always {
                    mail to: 'nikhilnaga2@gamil.com',
                         subject: "Security Scan Results: ${currentBuild.currentResult}",
                         body: "The security scan has completed with status: ${currentBuild.currentResult}. Please review the scan results.",
                         attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Deploy to staging server (e.g., using SSH)
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy'
                sh 'ssh user@staging-server "systemctl restart myapp"'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Run Selenium or other integration tests on staging environment
                sh 'mvn verify -P staging-integration-tests'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Deploy to production server (e.g., using SSH)
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy'
                sh 'ssh user@production-server "systemctl restart myapp"'
            }
        }
    }

    post {
        failure {
            mail to: 'nikhilnaga2@gmail.com',
                 subject: "Jenkins Build Failed: ${currentBuild.fullDisplayName}",
                 body: "The Jenkins build has failed. Please review the logs for more details.",
                 attachLog: true
        }
    }
}
