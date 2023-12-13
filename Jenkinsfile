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
                    // Переход в каталог с docker-compose.yml
                    dir("~/home/puzik/Diplom") {
                        sh 'docker-compose up -d'
                        sleep 30
                    }
                }
            }
        }

        stage('Configure Nginx') {
            steps {
                script {
                    sleep 20
                    def nginxContainerId = sh(script: 'docker-compose ps -q nginx', returnStdout: true).trim()
                    sh "docker inspect --format='{{.State.Running}}' $nginxContainerId"
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
