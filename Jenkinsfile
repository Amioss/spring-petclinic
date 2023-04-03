pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                sh './mvnw spring-boot:run -Dspring-boot.run.profiles=mysql'
                echo 'Build and Test succeeded!'
            }
        }
    }
}
