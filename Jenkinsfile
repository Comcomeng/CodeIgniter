pipeline {
    agent any

    environment {
        CI_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'develop', url: 'https://github.com/Comcomeng/CodeIgniter.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'composer install --no-dev --optimize-autoloader'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'phpunit'
            }
            post {
                success {
                    junit 'application/tests/results/*.xml'
                }
                failure {
                    echo 'Tests failed!'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to production environment...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
