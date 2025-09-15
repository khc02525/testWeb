pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5050"
        IMAGE_NAME = "my-tomcat-app"
        DOCKERFILE_PATH = "tomcat/Dockerfile"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/khc02525/testWeb.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                    docker build -t localhost:5000/my-tomcat-app:latest -f tomcat/Dockerfile .
                    """
                }
            }
        }

        stage('Push to Local Registry') {
            steps {
                script {
                    sh """
                    docker push localhost:5000/my-tomcat-app:latest
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh """
                    docker compose -f docker-compose.yml up -d --build
                    """
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
    }
}

