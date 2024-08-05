pipeline {
    agent any
    environment {
        IMAGE_NAME = 'paymentservice'
        IMAGE_TAG = 'v0.1.0'
        AWS_REGION = 'ap-southeast-1'
        REGISTRY_URL = "010438465474.dkr.ecr.${AWS_REGION}.amazonaws.com/microservice-demo"
    }
    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'aws-root', usernameVariable: "AWS_ACCESS_KEY_ID", passwordVariable: "AWS_SECRET_ACCESS_KEY")]) {
                        sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${REGISTRY_URL}"
                        sh "docker build -t ${REGISTRY_URL}:${IMAGE_NAME}-${IMAGE_TAG} ."
                        
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'aws-root', usernameVariable: "AWS_ACCESS_KEY_ID", passwordVariable: "AWS_SECRET_ACCESS_KEY")]) {
                        sh "docker push ${REGISTRY_URL}:${IMAGE_NAME}-${IMAGE_TAG}"
                    }
                }
            }
        }
    }
}
