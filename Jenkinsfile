pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-node-app' // Your Docker image name
        DOCKER_HUB_REPO = 'exampleuser/my-node-app' // Your Docker Hub repository name
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'
        PATH = "$PATH:/snap/bin/"
         DOCKER_HUB_REPO = 'sr88007/my-node-app'
    }

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', credentialsId: '7c139a60-3c2b-4181-b1c4-4b86e25e4ff7', url: 'https://github.com/SR-Rajput/Node-Demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('my-node-app')
                }
            }
        }

       stages {
        stage('Push Docker Image') {
            steps {
                script {
                    // Tag Docker image
                    docker.image(DOCKER_IMAGE).tag("${DOCKER_HUB_REPO}:latest")

                    // Push Docker image to Docker Hub
                    docker.withRegistry('', 'docker-hub-credentials') {
                        docker.image("${DOCKER_HUB_REPO}:latest").push()
                    }
                }
            }
        }
    }
}
