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
               bat 'npm -v'
               bat 'node -v'
            }
        }
        stage("build"){
            steps{
               bat 'npm run start'
            }
        }
    }
}
