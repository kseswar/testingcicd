pipeline {
	 environment {
	    registry = "280994/firstrepo"
	    registryCredential = 'dockerhub'
	    app = ''
  	}
	agent any
	    stages {
	        stage('Clone Repository') {
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build Docker Image') {
	        steps {
				script {
				 app = docker.build registry +":latest"
				 app.inside {
					sh 'echo $(curl localhost:8888)'
				 }
				}
	        }
	   }
	   stage('Run Image') {
	        steps {
	        sh 'docker run -d -p 5000:5000 280994/firstrepo:latest'
	        }
	   }

	   stage('Testing') {
	        steps {
	            echo 'Testing..'
	            }
	   }

	   stage('Push Docker image') {
	        steps {
                   script {
		    docker.withRegistry( '', registryCredential ) {
            	    app.push()
			}
	        }

	   }
	 }
    }
}
