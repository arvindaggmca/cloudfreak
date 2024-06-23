pipeline {
  agent any
   environment {
        DOCKER_REGISTRY = "https://myazregistry06222024.azurecr.io"
    }
    
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
         
	stage('Build') {
            steps {
                script {
                    docker.build('petclinic:latest')
                }
            }
        }
        
        stage('Push') {
            steps {
                script {
                    docker.withRegistry(env.DOCKER_REGISTRY, 'acr-demo') {
                        docker.image('petclinic:latest').push()
                    }
                }
            }
        }
	  
	  
	  
    }
}
