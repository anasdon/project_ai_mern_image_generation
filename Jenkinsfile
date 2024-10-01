pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Client Tests') {
            steps {
                dir('client') {
                    sh 'npm install'
                }
            }
        }
        stage('Server Tests') {
            steps {
                dir('server') {
                    sh 'npm install'
                }
            }
        }
        stage('Build Images') {
            steps {
                sh 'sudo docker build -t front-end:latest client'
                sh 'sudo docker build -t back-end:latest server'

            }
        }
        stage('Push Images to Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub' , passwordVariable: 'DOCKER_PASSWORD' , usernameVariable: 'DOCKER_USERNAME')]) {
                        sh 'sudo docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'sudo docker push front-end:v1'
                        sh 'sudo docker push back-end:v1'
                }
            }
        }
    }
}    
