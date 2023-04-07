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
                    docker.build("${env.DOCKER_IMAGE_NAME}:latest", "--file=./Dockerfile --no-cache .")
                }
            }
        }
        stage('Test') {
            steps {
                echo "Test in progress..."
            }
        }
        stage('Run Petclinic in container ') {
            steps {
                sh "docker rm -f petclinic_container || true"
                sh "docker run -d --name petclinic_container -p 80:8080 ${env.DOCKER_IMAGE_NAME}:latest"
            }
        }
    }
    post {
        always {
            sh "docker ps -a"
        }
    }
}
