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
                bat 'docker build -t pitchairaman/nodeapp:$latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                bat 'docker push pitchairaman/nodeapp:$latest'
            }
        }
}
post {
        always {
            bat 'docker logout'
        }
    }
}
