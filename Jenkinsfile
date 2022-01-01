pipeline {
    agent any 
    environment {
        DOCKER_TAG = getDockerTag()
        registry = "sharksdocker/nodeapp"
        registryCredential = "sharkshub"
    }
    stages {
        stage ('Build docker image') {
            steps {
                sh "docker build . -t sharksdocker/nodeapp:${DOCKER_TAG}"
            }
        }
        stage ('Push docker image') {
            steps {
                script {
                    docker.withRegistry('',registryCredential){
                    sh "docker push sharksdocker/nodeapp:${DOCKER_TAG}"
            }
            }
        }
        }
    }
}
def getDockerTag() {
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}



