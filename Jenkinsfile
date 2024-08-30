pipeline{
    agent any

    stages{
        stage('Build'){
            steps {
                echo'Build'
                sh 'fjao;psf'
            }
        }
    }
    post{
        success{
            emailext attachLog: true, body: 'This stage is ${env.BUILD.NUMBER}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
        }
        failure{
            emailext attachLog: true, body: 'This stage is ${BUILD.NUMBER}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'nikhilnaga2@gmail.com'
        }
    }
}

            
