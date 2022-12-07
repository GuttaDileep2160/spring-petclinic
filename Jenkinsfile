pipeline {
    agent any
    environment {
        imagename = 'spring-petclinic'
        dockerImage = ''
        CONTAINER_ID = ''
        dockerRegistry = 'gdileep/demo-spring_petclinic'
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn deploy; pwd'
            }
        }
        stage('Build docker image') {
            steps {
                script{
                    sh 'cd /var/lib/jenkins/workspace/project-pipeline'
                    sh "docker build -t ${imagename}:${BUILD_ID} ."
                }
            }
        }
        stage('Push docker image') {
            steps {
                script{
                    sh "docker tag ${imagename}:${BUILD_ID} ${dockerRegistry}:${BUILD_ID}"
                    sh "docker push ${dockerRegistry}:${BUILD_ID}"
                }
            }
        }
        stage('Deploy') {
            steps {
                script{
                    sh "docker run -d -p 9090:8080 ${imagename}:${BUILD_ID}"
                    
                }
              
              
            }
        }
    }
    post{
        success{
            sh "pwd"
            archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
        }
        
   }
}
