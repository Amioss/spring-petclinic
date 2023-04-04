#!groovy

pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'python:latest'
        }
      }
      steps {
        sh './mvnw spring-boot:run -Dspring-boot.run.profiles=mysql'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'sudo docker build -t amioss/app_petclinic:1.0 .'
      }
    }
  }
}
