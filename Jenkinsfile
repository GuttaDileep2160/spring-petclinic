pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage("Build"){
            steps{
                sh 'mvn install'
                sh 'pwd'
            }
        }
       stage("Build docker image"){
            steps{
                script {
                        dockerImage = docker.build imagename
                        }
                
            }
        }
}
}
