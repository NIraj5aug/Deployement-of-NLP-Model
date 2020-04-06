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
			    /***sh 'sudo docker stop nlpmodel'
			    sh 'sudo docker rm nlpmodel'  
			    sh 'sudo docker image prune -f'  ***/
			    sh 'sudo docker build -t niraj5aug/mynlpmodel:$BUILD_NUMBER .'
		
                }
	  }

          stage('Docker Push') {
          steps {

          withCredentials([usernameColonPassword(credentialsId: 'DockerHUB', variable: 'dockerhub')]) {
		  sh "docker login -u niraj5aug -p {$dockerhub}"
                   }
		   sh "docker push mynlpmodel:$BUILD_NUMBER"
                
                }
     }

	  stage('Run Image') {
	       steps {
	        sh 'sudo docker run -d -p 5000:4000 --name mymodel mynlpmodel:v1'
            }
		  
	   }
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}
