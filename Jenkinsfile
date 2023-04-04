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
        sh 'sudo mvn clean install'
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
