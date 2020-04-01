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
		sh 'sudo docker build -t mynlpmodel:v1 .'
		
	        // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'jfrog-docker', url: 'http://52.183.129.20:8082/ui/admin/repositories/local/dockerrepo/') {
                // some block
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
