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
                    sleep 30 // Подождем 30 секунд для полного запуска сервисов (можно регулировать время)
                }
            }
        }

        stage('Configure Nginx') {
            steps {
                script {
                    // Даем немного времени на запуск сервисов
                    sleep 20

                    // Получаем ID контейнера nginx
                    def nginxContainerId = sh(script: 'docker-compose ps -q nginx', returnStdout: true).trim()

                    // Проверяем, что контейнер nginx запущен
                    sh "docker inspect --format='{{.State.Running}}' $nginxContainerId"

                    // Запускаем конфигурацию nginx
                    sh "docker exec $nginxContainerId /bin/bash -c \"echo 'proxy_pass http://apache:8083;' > /etc/nginx/conf.d/default.conf\""
                }
            }
        }
    }

        post {
        success {
            script {
                echo 'Pipeline completed successfully'
            }
        }
    }
}
