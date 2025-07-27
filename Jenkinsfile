pipeline{
    agent any
    tools {
       nodejs 'node18'
    }
    environment {
        DEPLOYMENT_NAME = 'my-app-deployment'
        HTTP_PROXY = 'http://proxy.example.com:8080'
        HTTPS_PROXY = 'http://proxy.example.com:8080'
        NO_PROXY = 'localhost,127.0.0.1,docker.io'
        KUBECONFIG = credentials('kubeconfig')
    }
    stages {
        stage("checkout"){
            steps{
               checkout scm
            } 
        }
        stage("test"){
              steps{
                 bat 'npm -v'
                 bat 'node -v'
             }
          }
        stage("build"){
            steps{
               bat 'echo "running build script" '
            }
        }
        stage("build Image"){
            steps{
                bat 'docker build -t my-node-pipe:1.0 .'
            }
        }
        stage("docker push image"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker_cred' , passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]){
                bat ' echo %DOCKERHUB_PASSWORD% | docker login -u %DOCKERHUB_USERNAME% --password-stdin'
                bat 'docker tag my-node-pipe:1.0 abhiattri/my-node-pipe:1.0'
                bat 'docker push abhiattri/my-node-pipe:1.0'
                bat 'docker logout'
               }
            }
        } 
        stage('Check Minikube Status') {
            steps {
                script {
                    bat 'kubectl version'
                    bat 'minikube status'
                }
            }
        }
        stage("deployment"){
            steps{
                bat 'kubectl create deployment $DEPLOYMENT_NAME --image=abhiattri/my-node-pipe:1.0 --kubeconfig=$KUBECONFIG'
                bat 'kubectl expose deployment $DEPLOYMENT_NAME --type=LoadBalance --kubeconfig=$KUBECONFIG'
            }
        }
        stage("verify pods running"){
            steps{
                bat 'kubectl get pods --kubeconfig=$KUBECONFIG'
            }
        }
    }
}
