pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker_login')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/PitchairamanJobs/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t pitchairaman/nodeapp:$latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push pitchairaman/nodeapp:$latest'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
