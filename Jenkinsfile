pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Install Docker
                    sh 'curl -fsSL https://get.docker.com/ | sh'

                    // Sleep for 20 seconds to wait for Docker to install
                    sleep(time: 20, unit: 'SECONDS')

                    // Run Docker-compose
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            echo 'This runs always'
            // Update packages
            sh 'apt-get update -qq'
        }
    }
}
