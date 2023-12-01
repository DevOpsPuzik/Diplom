pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_VERSION = '1.29.2'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            script {
                // Ждем, чтобы сервисы полностью развернулись перед выполнением тестов
                sleep 60
                // Запуск тестов, проверяющих, что запросы на Nginx перенаправляются в Apache
                sh 'curl http://localhost'
            }
        }

        success {
            // Шаги, которые выполнятся при успешном разворачивании и прохождении тестов
            echo 'Deployment and tests passed successfully!'
        }

        failure {
            // Шаги, которые выполнятся в случае ошибки в разворачивании или тестах
            echo 'Deployment or tests failed!'
        }
    }
}
