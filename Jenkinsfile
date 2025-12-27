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
                script {
                    docker.build("cicd-node-service:${env.BUILD_ID}")
                }
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