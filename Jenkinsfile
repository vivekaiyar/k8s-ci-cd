pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        ImageName = ImageName()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t ${ImageName}:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push'){
            steps{
                script {
                docker.withRegistry("http://art4lab0.labs.mastercard.com:5001", 'art4lab0-docker-deploy') {
                    //sh "docker login -u deploy -p ${docker_deploy} http://art4lab0.labs.mastercard.com"
                    sh "docker tag ${ImageName}:${DOCKER_TAG} artifactory/list/docker-internal/test/${ImageName}:${DOCKER_TAG}"
                    sh "docker push artifactory/list/docker-internal/test/${ImageName}:${DOCKER_TAG}"
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
    def tag = "artifactory/list/docker-internal/test/nodeapp"
    return tag
}
 
