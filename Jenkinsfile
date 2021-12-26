pipeline {
    agent any 
    stages {
        stage('Build') {
            dir('infrastructure') {
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