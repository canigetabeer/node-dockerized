pipeline{
    agent any
    stages {
     stage("checkout"){
        setps{
            checkout scm
        } 
    }
    stage("test"){
        steps{
            sh 'sudo npm install'
        }
    }
    stage("build"){
        steps{
            sh 'npm run start'
        }
    }
}
}
