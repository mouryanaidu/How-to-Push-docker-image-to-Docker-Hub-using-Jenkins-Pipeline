pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('mou_dockid')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/mouryanaidu/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t mouryanaidu/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push mouryanaidu/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
