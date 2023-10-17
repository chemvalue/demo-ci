pipeline {

    agent {label 'agent1'}

    stages {

        stage('Deploy Spring Boot to DEV') {
            steps {
                echo 'Deploying and cleaning'
            }
        }
 
    }
    post {
        // Clean after build
        always {
            cleanWs()
        }
    }

}
