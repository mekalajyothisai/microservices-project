pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t jyothisaimekala/frontend:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push jyothisaimekala/frontend:latest"
                    }
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
