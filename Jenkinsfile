pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-credential')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/sosotechnologies/december-pipeline.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t sosotech/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push sosotech/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
