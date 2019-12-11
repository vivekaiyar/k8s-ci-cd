pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t node/nodeapp:${DOCKER_TAG} "
            }
        }
        stage('DockerHub Push'){
            steps{
                withCredentials([usernameColonPassword(credentialsId: 'art4lab0-docker-deploy', variable: 'docker_deploy')]) {
                    sh "docker login -u deploy -p ${docker_deploy}"
                    sh "docker push node/nodeapp:${DOCKER_TAG}"
                }
            }
        }
        

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
    }
