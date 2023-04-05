pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "petclinic_app"
        DOCKERFILE_GITHUB_REPO = "https://github.com/Amioss/spring-petclinic.git"
        DOCKERFILE_GITHUB_BRANCH = "main"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.DOCKERFILE_GITHUB_BRANCH}", url: "${env.DOCKERFILE_GITHUB_REPO}"
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    docker.build("${env.DOCKER_IMAGE_NAME}:latest", "--file=./Dockerfile .")
                }
            }
        }
        stage('Run Docker container') {
            steps {
                sh "docker run -d -p 8080:8080 ${env.DOCKER_IMAGE_NAME}:latest"
            }
        }
    }
    post {
        always {
            sh "docker ps -a"
        }
    }
}
