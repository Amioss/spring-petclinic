pipeline {
  agent none
  stages {
    stage('Spring Boot Run') {
      agent any
      steps {
        script {
          def appStatus = sh script: './mvnw spring-boot:run -Dspring-boot.run.profiles=mysql', returnStatus: true
          if (appStatus == 0) {
            echo "Success: Application started successfully"
          } else {
            echo "Error: Application failed to start"
            error "Failed to start application"
          }
        }
      }
    }
    stage('Docker Build') {
      when {
        expression {
          return appStatus == 0
        }
      }
      agent any
      steps {
        sh 'docker build -t amioss/app_petclinic:1.0 .'
      }
    }
  }
}
