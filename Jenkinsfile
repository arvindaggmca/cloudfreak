pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK11'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
		
		stage('Login to ACR') {
            steps {
                script {
                    docker.withRegistry('myazregistry06222024.azurecr.io', 'acr-demo') {
                        // Use the Docker image for subsequent steps
                    }
                }
            }
        }
         
stage('Build and Push Image') {
            steps {
                script {
                    // Building a Docker image from a Dockerfile in the current directory
                    def customImage = docker.build("myazregistry06222024.azurecr.io/arvindaggmca/petclinic:${env.BUILD_ID}")
                    // Pushing the image to ACR
                    customImage.push()
                }
            }
        }
	  
	  
	  
    }
}
