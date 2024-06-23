pipeline {
    agent any
    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://myazregistry06222024.acr.io', 'acr-demo') {
                        // Assuming 'myazregistry06222024-credentials' is the ID of the credentials you have configured.
                        def app = docker.build("myapp:${env.BUILD_ID}")
                        app.push()
                    }
                }
            }
        }
    }
}
