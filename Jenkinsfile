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
                    sh 'cd client'
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        } 
    }
}    