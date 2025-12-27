pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from Git...'
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t cicd-node-service:${BUILD_ID} .'
                sh 'docker tag cicd-node-service:${BUILD_ID} cicd-node-service:latest'
            }
        }
        
        stage('Verify Build') {
            steps {
                echo 'Verifying Docker image was created...'
                sh 'docker images | grep cicd-node-service'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}