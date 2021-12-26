pipeline {
    agent any 
    stages {
        stage('Build') {
         steps {
            dir('infrastructure') {
                 sh 'docker-compose build'
                }
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