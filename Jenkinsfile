pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-node-app' // Your Docker image name
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'
        PATH = "$PATH:/snap/bin/"
        DOCKER_HUB_REPO = 'sr88007/my-node-app' // Your Docker Hub repository name
         AWS_SERVER_IP = '65.2.130.30'
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
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    // Docker login using credentials from Jenkins
                    withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS, passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    }
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    // Tag Docker image
                    sh "docker tag ${DOCKER_IMAGE} ${DOCKER_HUB_REPO}"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    sh "docker push ${DOCKER_HUB_REPO}"
                }
            }
        }
    
    

        stage('Deploy on AWS Jenkins Server') {
            steps {
                // Pull Docker image from Docker Hub to /home directory on AWS Jenkins server
                withCredentials([sshUserPrivateKey(credentialsId: 'aws-credentials', keyFileVariable: 'SSH_KEY_FILE', usernameVariable: 'SSH_USERNAME')]) {
                       sh """
                ssh -i ${SSH_KEY_FILE} ${SSH_USERNAME}@${AWS_SERVER_IP} '
                    sudo docker pull ${DOCKER_HUB_REPO} &&
                    sudo docker-compose -f /home/docker-compose.yaml up -d
                '
            """
                }
            }
        }
    }
}
