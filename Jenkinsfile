pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests=true -Dspring.profiles.active=mysql'
            }
        }
        
        
    }
}
