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
                    sleep 30  // Подождем 30 секунд для полного запуска сервисов (можно регулировать время)
                }
            }
        }

        stage('Configure Nginx') {
            steps {
                script {
                    // Используем правильное имя контейнера
                    sh 'docker exec diplom2_nginx_1 /bin/bash -c "echo \\"proxy_pass http://apache:8083;\\" > /etc/nginx/conf.d/default.conf"'
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
