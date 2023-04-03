pipeline {
    agent {
        label 'JDK17'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        retry(2)
    }
    stages {
        stage('Source code') {
            steps {
                git url: 'https://github.com/Amioss/spring-petclinic.git', branch: 'main'
            }
        }
        stage('Build the code') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('Reporting and Archiving') {
            steps {
                junit testResults: 'target/surefire-reports/*.xml'
            }
        }
    }
    post {
        success {
            //send the success email
            echo "success"
        }
        unsuccessful {
            //send the unsuccessful email
            echo "Failure"
        }
    }
}
