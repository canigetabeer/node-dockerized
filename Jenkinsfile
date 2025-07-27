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
            sh 'sudo apt install npm'
        }
    }
    stage("build"){
        steps{
            sh 'npm run start'
        }
    }
}
}
