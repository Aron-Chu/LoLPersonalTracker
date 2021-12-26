pipeline {
    agent any 
    stages {
        stage('CD') {
            steps {
                sh 'cd infrastructure'
                sh 'ls'
            }
        }
        stage('Build') {
            steps {
                sh 'docker-compose build'
                }
        }
        stage('Run') {
            steps {
                sh 'docker-compose up -d'
            }
        }
        stage('Destroy') {
            steps {
             sh 'docker-compose down -v'
            }
        }
    }
}