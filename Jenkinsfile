pipeline{

   agent any

	//create dockerhub credential in github with TOKEN
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git 'https://github.com/febfun1/NovClass.git'
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t febfun/class_app:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username febfun --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push febfun/class_app:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}

