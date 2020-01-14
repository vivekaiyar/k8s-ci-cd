pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        ImageName = ImageName()
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
                docker.withRegistry("https://art4lab0.labs.mastercard.com:8081", 'art4lab0-docker-deploy') {
                    //sh "docker login -u deploy -p ${docker_deploy} http://art4lab0.labs.mastercard.com"
                    sh "docker tag node/nodeapp:latest art4lab0.labs.mastercard.com:5001/artifactory/infra-docker/test/node/nodeapp:v1"
                    sh "docker push art4lab0.labs.mastercard.com:5001/artifactory/infra-docker/test/node/nodeapp:v1"
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
def ImageName(){
    def tag = "node/nodeapp"
    return tag
}
