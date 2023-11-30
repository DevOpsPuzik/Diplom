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
                    // Установка Docker и Docker Compose
                    sh 'curl -fsSL https://get.docker.com/ | sh'
                    sh "sudo curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose"
                    sh 'sudo chmod +x /usr/local/bin/docker-compose'
                    
                    // Запуск Docker Compose для разворачивания сервисов
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            // Завершающий шаг - можно добавить тут дополнительные проверки, логирование и т. д.
        }
    }
}
