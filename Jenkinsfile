pipeline{
    agent any
    tools {
       nodejs 'node18'
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
               bat 'node index.js'
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
    }
}
