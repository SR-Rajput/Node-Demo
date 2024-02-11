pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               git branch: 'main', credentialsId: '7c139a60-3c2b-4181-b1c4-4b86e25e4ff7', url: 'https://github.com/SR-Rajput/demo-app.git'
            }
        }
    }
}
