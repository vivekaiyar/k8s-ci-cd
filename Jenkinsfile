pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t node/nodeapp:v1"
            }
        }
        stage('DockerHub Push'){
            steps{
                script {
                docker.withRegistry('https://art4lab0.labs.mastercard.com:5001', 'art4lab0-docker-deploy') {
                    //sh "docker login -u deploy -p ${docker_deploy} http://art4lab0.labs.mastercard.com"
                    sh "docker tag node/nodeapp:v1 art4lab0.labs.mastercard.com:5001/artifactory/docker-internal/test/node/nodeapp:v1"
                    sh "docker push art4lab0.labs.mastercard.com:5001/artifactory/docker-internal/test/node/nodeapp:v1"
                }
                }
            }
        }
    }
}        

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
    }
 
