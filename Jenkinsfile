pipeline {
    agent none
    stages {
	stage('Packaging/Pushing image') {
	    agent {label 'agent-ci'}
            steps {
                withDockerRegistry(credentialsId: 'docker-registry', url: 'https://docker-test.nguyenlinh2.site') {
                    sh 'docker build -t docker-test.nguyenlinh2.site/demo-laravel .'
                    sh 'docker push docker-test.nguyenlinh2.site/demo-laravel'
                }
            }
        }
	stage('Deploy container with ansible') {
            agent{label 'ansible-agent'}
	    environment {
        	ANSIBLE_HOST_KEY_CHECKING = 'False'
    	    }
	    steps {
                withCredentials([file(credentialsId: 'ansible_key', variable: 'ansible_key')]) {
                    sh 'ls -la'
                    sh "cp /$ansible_key ansible_key"
                    sh 'cat ansible_key'
                    sh 'ansible --version'
                    sh 'ls -la'
                    sh 'chmod 400 ansible_key '
                    sh 'ansible-playbook -i hosts --private-key ansible_key playbook.yml'
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
