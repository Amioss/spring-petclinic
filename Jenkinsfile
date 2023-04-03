pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh './mvnw spring-boot:run -Dspring.profiles.active=mysql'
            }
        }
    }
}
