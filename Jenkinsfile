pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                ./mvnw spring-boot:run -Dspring-boot.run.profiles=mysql
            }
        }
}
}
