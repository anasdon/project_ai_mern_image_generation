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
                sh 'docker build -t front-end/AI-App:client:latest client'
                sh 'docker build -t back-end/AI-App:server:latest server'

            }
        }
        stage('Push Images to Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub' , passwordVariable: 'DOCKER_PASSWORD' , usernameVariable: 'DOCKER_USERNAME')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker push front-end/AI-App:client:latest'
                        sh 'docker push back-end/AI-App:server:latest'
                }
            }
        }
    }
}    