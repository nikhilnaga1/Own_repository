pipeline{
    agent any

    stages{
        stage('Build'){
            steps {
                echo'Build'
            }
        }
    }
    post{
        success{
            emailext attachLog: true, body: 'This stage is ${env.BUILD.NUMBER}', subject: '', to: 'nikhilnaga2@gmail.com'
        }
        failure{
            emailext attachLog: true, body: 'This stage is ${BUILD.NUMBER}', subject: '', to: 'nikhilnaga2@gmail.com'
        }
    }
}

            
