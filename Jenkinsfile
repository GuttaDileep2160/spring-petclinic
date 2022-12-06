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
                sh 'mvn install'
                sh 'pwd'
            }
        }
        stage('Build docker image') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/project-pipeline'
                sh "docker build -t ${imagename}:${BUILD_ID} ."
            }
        }
        stage('Push docker image') {
            steps {
                sh "docker tag ${imagename}:${BUILD_ID} ${dockerRegistry}:${BUILD_ID}"
                sh "docker push ${dockerRegistry}:${BUILD_ID}"
            }
        }
    }
}
