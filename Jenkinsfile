pipeline {

    agent {label 'agent1'}

    stages {

	stage('Packaging/Pushing image') {

            steps {
		echo 'Start build docker image'
                withDockerRegistry(credentialsId: 'docker-registry', url: 'https://docker-test.nguyenlinh2.site') {
		    echo 'Login success'
                    sh 'docker build -t docker-test.nguyenlinh2.site/demo-laravel .'
                    sh 'docker push docker-test.nguyenlinh2.site/demo-laravel'
		    echo 'After push'
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
