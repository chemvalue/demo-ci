pipeline {

    agent {label 'agent1'}

    stages {

        stage('Deploy Spring Boot to DEV') {
            steps {
                echo 'Deploying and cleaning'
            }
        }

	stage('Packaging/Pushing image') {

            steps {
                withDockerRegistry(credentialsId: 'docker-registry', url: 'https://docker-test.nguyenlinh2.site') {
                    sh 'docker build -t docker-test.nguyenlinh2.site/demo-laravel .'
                    sh 'docker push docker-test.nguyenlinh2.site/demo-laravel'
                }
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
