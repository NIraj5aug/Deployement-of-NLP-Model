pipeline {
	agent { label 'Ansible' }
	    stages {
	        stage('Clone Repository') {
	        /* Cloning the repository to our workspace */
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build Image') {
	        steps {
			sh 'sudo docker stop nlpmodel'
			sh 'sudo docker rm nlpmodel'
			sh 'sudo docker image prune -y'
			sh 'sudo docker build -t mynlpmodel:v1 .'
		
                }
	  }
	  stage('Run Image') {
	       steps {
	        sh 'sudo docker run -d -p 5000:4000 --name nlpmodel mynlpmodel:v1'
            }
		  
	   }
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}
