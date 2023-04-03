pipeline {
    agent any
    
    stages {
        stage('Buildd') {
            steps {
                sh './mvnw clean package -DskipTests=true -Dspring.profiles.active=mysql'
            }
        }
        
        
    }
}
