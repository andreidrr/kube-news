pipeline {
    agent any 


    stages {

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("andreidrr/kube-news:${env.BUILD_id}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Docker Image'){
            steps {
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push ('latest')
                        dockerapp.push ("${env.BUILD_id}")
                    }
                    
                }
            }
        }


        stage ('Deploy Kubernets'){
            steps{
                withKubeconfig ([credenccredentialsId: 'kubeconfig']){
                    sh 'kubectl apply -f ./k8s/deployment.yaml'

                }
            }
        }

    }
}