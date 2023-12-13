pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build and Run Docker Compose') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Configure Nginx') {
            steps {
                script {
                         sleep 20
                    sh 'docker exec puzik_nginx_1 /bin/bash -c "echo \\"proxy_pass http://apache:8082;\\" > /etc/nginx/conf.d/default.conf"'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker-compose down'
            }
        }
    }
}
