pipeline {
  agent none
  stages {
    stage('Spring Boot Run') {
      agent any
      steps {
        sh './mvnw spring-boot:run -Dspring-boot.run.profiles=mysql'
        echo "success"
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t amioss/app_petclinic:1.0 .'
      }
    }
  }
}
