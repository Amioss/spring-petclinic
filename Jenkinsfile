pipeline {
  agent {
    docker {
      image 'maven:3.8.3-openjdk-17-slim'
      args '-v $HOME/.m2:/root/.m2'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
  }
}
