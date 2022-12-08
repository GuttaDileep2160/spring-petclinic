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
                sh 'mvn install -DskipTests; pwd'
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
                
                    sh "docker run -d -p 9090:8080 ${imagename}:${BUILD_ID}"
                    sh "sleep 10"
                    sh 'docker ps'
                    sh "CONTAINER_ID=`docker ps | grep java | awk '{print $1}'`"
                    sh "echo $CONTAINER_ID"
                    sh "docker stop $CONTAINER_ID"
                
              
              
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
