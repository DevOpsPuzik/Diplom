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
                    sleep 23  // Увеличьте время ожидания до 23 секунд (или более) для полного запуска сервисов
                    sh 'docker-compose ps'
                    sh 'docker-compose logs'  // Посмотрите логи контейнеров
                }
            }
        }

        stage('Configure Nginx') {
            steps {
                script {
                    // Используем правильное имя контейнера
                    sh 'docker exec diplom_nginx_1 /bin/bash -c "echo \\"proxy_pass http://apache:8083;\\" > /etc/nginx/conf.d/default.conf"'
                }
            }
        }
    }
}
