pipeline {
    agent any
    environment {
        IMAGE_NAME = 'bbc-new'
        CONTAINER_NAME = 'site'
        }
    
    stages {  
    stage('Git check') { 
        steps {
        git branch: 'main', url: 'https://github.com/harikrishnan-knr/BBC_News_Website.git'
        }
    }

    stage('Build') {
        steps {
        sh '''docker -v
        docker build -t ${IMAGE_NAME} .'''
        }
    }
        
    stage('Stop Old Container') {
        steps {
        sh 'docker stop ${CONTAINER_NAME} || true'
        sh 'docker rm -f ${CONTAINER_NAME} || true'
            }
        }
        
    stage('Run') { 
        steps {
        sh '''docker run -d --name ${CONTAINER_NAME} -p 80:80 ${IMAGE_NAME}:latest
        docker ps'''
        }
    }
    }
}
