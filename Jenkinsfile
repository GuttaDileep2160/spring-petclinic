pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage("Build"){
            steps{
                sh 'cd /project-pipeline/src'
                sh 'mvn install'
            }
        }
       
}
}
