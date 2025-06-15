pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://18AC1CAC6969818723A4E8995000FD84.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-2', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', serverUrl: 'https://18AC1CAC6969818723A4E8995000FD84.gr7.us-east-1.eks.amazonaws.com']]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
    post{
       always {
             echo 'Slack Notifications'
                     slackSend (channel: 'e-commerce-app', message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} \n  build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}")
     }
    }
}
