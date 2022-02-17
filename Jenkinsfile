pipeline {
    agent any 
    environment {
        DOCKER_ID = credentials('DOCKER_ID')
        DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')
    }
    stages {
        stage('Build') {
         steps {
            dir('infrastructure') {
                 echo '$BRANCH_NAME'
                 sh 'docker-compose build'
                }
            }
        }
        stage('Push') {
            steps {
                dir('infrastructure') {
                 sh 'docker login -u $DOCKER_ID -p $DOCKER_PASSWORD'
                 sh 'docker tag infrastructure_grafana girthquake1/infrastructure_grafana'
                 sh 'docker push girthquake1/infrastructure_grafana'
                 sh 'docker tag infrastructure_influxdb girthquake1/infrastructure_influxdb'
                 sh 'docker push girthquake1/infrastructure_influxdb'
                 sh 'docker tag infrastructure_nodered girthquake1/infrastructure_nodered'
                 sh 'docker push girthquake1/infrastructure_nodered'
                 sh 'docker tag nodered/node-red girthquake1/nodered'
                 sh 'docker push girthquake1/nodered'
                 sh 'docker tag grafana/grafana girthquake1/grafana'
                 sh 'docker push girthquake1/grafana'
                 sh 'docker tag influxdb girthquake1/influxdb'
                 sh 'docker push girthquake1/influxdb'
                 
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
                chmod 777 /var/run/docker.sock
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