pipeline {
    agent any
  
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mtulasi41/online-botique-deploy.git']])
            }
        }
        stage('Integrate Jenkins with EKS Cluster and Deploy App'){
            steps{
                withAWS(credentials: 'AwsCred', region: 'ap-south-1') {
                    script {
                        sh 'aws eks describe-cluster --region ap-south-1 --name my-eks-cluster --query cluster.status'
                        sh 'aws eks --region ap-south-1 update-kubeconfig --name my-eks-cluster'
                        sh "kubectl apply -f kubernetes-manifests.yaml"
                    }
                }
            }
        }   
                
    }
}
