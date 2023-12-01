pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Установка Docker
                    sh 'curl -fsSL https://get.docker.com/ | sh'

                    // Перенос пути установки Docker в PATH
                    sh 'export PATH="/usr/local/bin:$PATH"'

                    // Установка Docker Compose
                    sh 'sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                    sh 'sudo chmod +x /usr/local/bin/docker-compose'

                    // Запуск Docker Compose для разворачивания сервисов
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
