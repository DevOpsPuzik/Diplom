pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_VERSION = '1.29.2'
        SUDO_PASSWORD = 'your_sudo_password'
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

                    // Используйте параметр -S с командой sudo
                    sh "echo \$SUDO_PASSWORD | sudo -S curl -L https://github.com/docker/compose/releases/download/\${DOCKER_COMPOSE_VERSION}/docker-compose-\$(uname -s)-\$(uname -m) -o /usr/local/bin/docker-compose"
                    sh 'sudo chmod +x /usr/local/bin/docker-compose'

                    // Запуск Docker Compose для разворачивания сервисов
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            echo 'This runs always'
            // Добавьте дополнительные шаги или логирование здесь

            // Используйте параметр -S с командой sudo
            sh 'echo $SUDO_PASSWORD | sudo -E apt-get update -qq >/dev/null'
        }
    }
}
