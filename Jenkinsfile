pipeline {
    agent any 


    stages {

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.Build("andreidrr/kube-news:${env.BUILD_id}", '-f ./src/Dockerfile .src')
                }
            }
        }

    }
}