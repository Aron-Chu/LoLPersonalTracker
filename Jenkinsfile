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
            dir('infrastructure') {
                 sh 'docker-compose up -d'
                }
            }
        }
        stage('Destroy') {
         steps {
            dir('infrastructure') {
                 sh 'docker-compose down -v'
                }
            }
        }
    }
}