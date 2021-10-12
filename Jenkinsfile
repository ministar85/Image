pipeline {
    agent { label 'linux' }
	options { 
		buildDiscarder(logRotator(numToKeepStr: '5'))
	}
	enviroment {
		DOCKERHUB_CREDENTIALS = credentials('muehlbauer-dockerhub')
	}
	stages {
        stage('Build') {
            steps {
                sh 'docker build -t muehlbauer/ui-qms:0.0.40 .'
            }
        }
		stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
		stage('Push') {
            steps {
                sh 'docker push muehlbauer/ui-qms:0.0.40'
            }
        }
	}
	post {
		always {
			sh 'docker logout'
		}
	}
}