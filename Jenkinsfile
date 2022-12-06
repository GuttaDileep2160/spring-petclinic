pipeline {
    agent any
    environment {
        imagename = 'spring-petclinic'
        registryCredential = 'yenigul-dockerhub'
        dockerImage = ''
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
                script {
                        dockerImage = docker.build imagename:${BUILD_NUMBER}
                }
            }
        }
    }
}
