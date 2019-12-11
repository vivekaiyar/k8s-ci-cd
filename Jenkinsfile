pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t node/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
            steps{
                script {
                docker.withRegistry('https://art4lab0.labs.mastercard.com:5001', 'art4lab0-docker-deploy') {
                    //sh "docker login -u deploy -p ${docker_deploy} http://art4lab0.labs.mastercard.com"
                    sh "docker tag node/nodeapp:${DOCKER_TAG} art4lab0.labs.mastercard.com:5001/artifactory/docker-internal/node/nodeapp:${DOCKER_TAG}"
                    sh "docker push art4lab0.labs.mastercard.com:5001/artifactory/docker-internal/node/nodeapp:${DOCKER_TAG}"
                }
                }
            }
        }
    }
}        

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD | cut -c1,5', returnStdout: true
    return tag
    }
 
