pipeline {
    agent {
        label 'ec2'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Amioss/spring-petclinic.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("petclinic", ".")
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm petclinic ./mvnw test'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_LOGIN', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    script {
                        docker.withRegistry("https://registry.example.com", "docker-credentials") {
                            dockerImage.push()
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d --name petclinic -p 80:8080 -p 3306:3306 petclinic'
            }
        }

        stage('Install Java and Maven') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y openjdk-17-jdk openjdk-17-jre maven'
            }
        }

        stage('Run Application') {
            steps {
                sh 'cd spring-petclinic && ./mvnw spring-boot:run -Dspring-boot.run.profiles=mysql'
            }
        }
    }

    post {
        always {
            sh 'docker stop petclinic && docker rm petclinic'
        }
    }
}
