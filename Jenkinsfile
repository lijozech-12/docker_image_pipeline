pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_access')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/lijozech-12/docker_image_pipeline.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t nginxapp/nginxbuild:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push nginxapp/nginxbuild:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}