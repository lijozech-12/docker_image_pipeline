pipeline{
    agent any
    tools {
        maven 'maven'
        jdk 'Java'
    }
    environment{
        dockerhub=credentials('dockerhub')
    }

    stage('build image')
    {
        when{
            branch "prod"
        }
        steps{
            sh 'docker build -t capstone-img:1.01'
        }
    }
    stage('pushing to dockerhub')
    {
        when{
            branch "prod"
        }
        steps{
            sh 'docker tag capstone-img:1.01 naincykumari123/capston:1.01'
            sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

            sh 'docker push '
        }
    }
}