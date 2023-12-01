pipeline {
    agent any

    stages {
        stage('Build and Run Docker Compose') {
            steps {
                script {
                    // Шаги для сборки и запуска Docker Compose
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            // Шаги, которые выполняются всегда, даже если произошла ошибка
            script {
                // Шаги для перенаправления запросов с Nginx на Apache
                sh 'docker exec nginx /bin/bash -c "echo \\"proxy_pass http://apache:8081;\\" > /etc/nginx/conf.d/default.conf"'
                sh 'docker exec nginx /bin/bash -c "nginx -s reload"'
            }
        }
    }
}
