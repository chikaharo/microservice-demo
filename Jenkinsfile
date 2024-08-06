pipeline {
    agent any 

    stages {
        stage('Deploy to EKS') {
            steps {
                script {
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'microservice-cluster', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://AAD36433358CFB9DE04471570F88C5C5.gr7.ap-southeast-1.eks.amazonaws.com']]) {
                        sh "kubectl apply -f Kubernetes/deployment.yaml"
                    }
                }
            }
        }
        
        stage('verify deployment') {
            steps {
                script {
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'microservice-cluster', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://AAD36433358CFB9DE04471570F88C5C5.gr7.ap-southeast-1.eks.amazonaws.com']]) {
                        sh "kubectl get svc -n webapps"
                    }
                }
            }
        }
    }
}