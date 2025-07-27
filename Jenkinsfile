pipeline{
    agent any
    stages {
        stage("checkout"){
            steps{
               checkout scm
            } 
        }
        stage("test"){
            steps{
               bat 'npm install'
            }
        }
        stage("build"){
            steps{
               bat 'npm run start'
            }
        }
    }
}
