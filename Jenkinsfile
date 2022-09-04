pipeline{
    agent any
    tools {
        maven 'maven'
        jdk 'Java'
    }
    environment{
        dockerhub=credentials('dockerhub')
    }

    stage('Approval')
    {

    }

    stage('Docker build')
    {
        when{
            branch "prod"
        }
        steps{
            sh 'docker build -t nginxapp:1.1'
        }
    }
    stage('Approval')
    {
        when{
            branch "prod"
        }
        steps{
            sh 'docker tag nginxapp:1.1 lijozech123/nginxapp:1.1'
            sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

        }
    }
    stage('Docker push')
    {
        when{
            branch "prod"
        }
        steps{
            sh 'docker push'
        }
    }
}