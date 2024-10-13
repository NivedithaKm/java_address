pipeline {
    agent any
    tools {
        maven "Mymaven"
    }
   environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-niveditha052')
    }
    stages {
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/NivedithaKm/java_address.git'
            }
        }
        stage ('Maven Build') {
            steps{
                sh 'mvn clean package'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t niveditha052/cicd:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push niveditha052/cicd:$BUILD_NUMBER'
            }
        }
}
}
