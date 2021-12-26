pipeline {
    agent any 
    stages {
        stage('Build') {
         steps {
            dir('infrastructure') {
                 sh 'cat $BRANCH_NAME'
                 sh 'docker-compose build'
                }
            }
        }
        stage('Validate Run') {
            when {
                beforeInput true
                branch "dev"
            }
            input {
                message "Do you want to run these containers?"
                ok "Run containers."
            }
            steps {
                echo 'Run Accepted'
            }   
        }
        stage('Run') {
         steps {
            dir('infrastructure') {
                 sh 'docker-compose up -d'
                }
            }
        }
        stage('Validate Destroy') {
            when {
                beforeInput true
                branch "dev"
            }
            input {
                message "Do you want to destroy these containers?"
                ok "Destroy containers."
            }
            steps {
                echo 'Destroy Accepted'
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
    post {
        success {
            echo 'Success!'
        }
        failure {
            sh 'docker-compose down -v'   
        }
    }
}