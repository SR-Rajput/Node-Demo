pipeline {
    agent any

   environment {
        DOCKER_IMAGE = 'my-node-app' // Your Docker image name
        DOCKER_HUB_REPO = 'exampleuser/my-node-app' // Your Docker Hub repository name
    }

    
    stages {
        stage('checkout') {
            steps {
               git branch: 'main', credentialsId: '7c139a60-3c2b-4181-b1c4-4b86e25e4ff7', url: 'https://github.com/SR-Rajput/demo-app.git'
            }
        }
    

   
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        } }
}
