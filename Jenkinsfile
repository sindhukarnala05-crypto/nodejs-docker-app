pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodejs-app .'
            }
        }
        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop nodejs-app || true
                docker rm nodejs-app || true
                '''
            }
        }
        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name nodejs-app nodejs-app'
            }
        }
        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}