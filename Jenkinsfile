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
			    sh 'sudo docker stop mymodel'
			    sh 'sudo docker rm mymodel'  
			    sh 'sudo docker image prune -f'
			    sh 'sudo docker build -t niraj5aug/mynlpmodel:$BUILD_NUMBER .'
		
                }
	  }

          stage('Docker Push') {
          steps {

                  /***withCredentials([usernameColonPassword(credentialsId: 'DockerHUB', variable: 'dockerhub')]) {
		 sh "docker login -u niraj5aug -p {$dockerhub}"
                   } ***/
		   sh "docker push niraj5aug/mynlpmodel:$BUILD_NUMBER"
                
                }
     }

	  stage('Run Image') {
	       steps {
	        sh 'sudo docker run -d -p 5001:4000 --name mymodel niraj5aug/mynlpmodel'
            }
		  
	   }
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}
