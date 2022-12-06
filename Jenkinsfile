pipeline {
    agent any
    environment {
        imagename = 'spring-petclinic'
        dockerImage = ''
        CONTAINER_ID = ''
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn install'
                sh 'pwd'
            }
        }
        stage('Build docker image') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/project-pipeline'
                sh 'docker build -t coit-backend1:${BUILD_ID} .'            
            }
        }
    }
}
