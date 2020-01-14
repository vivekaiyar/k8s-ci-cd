pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        ImageName = ImageName()
        registry = "http://art4lab0.labs.mastercard.com:5001/artifactory/list/docker-internal/test/"
        registryCredential = 'art4lab0-docker-deploy'
        dockerImage = ''
    }
    stages{
        stage('Build Docker Image'){
            steps{
                dockerImage = docker.build registry + "${ImageName}:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
            steps{
                script {
                docker.withRegistry( '', registryCredential) {
                    //sh "docker login -u deploy -p ${docker_deploy} http://art4lab0.labs.mastercard.com"
                    //sh "docker tag ${ImageName}:${DOCKER_TAG} art4lab0.labs.mastercard.com:5001/artifactory/list/docker-internal/test/${ImageName}:${DOCKER_TAG}"
                    //sh "docker push art4lab0.labs.mastercard.com:5001/artifactory/list/docker-internal/test/${ImageName}:${DOCKER_TAG}"
                    dockerImage.push()
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
 
