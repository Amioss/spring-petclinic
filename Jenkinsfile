pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.5.0'
                }
            }
            steps {
                sh 'mvn clean install -DskipTests=true -B'
            }
        }
        stage('Build container') {
            agent any
            steps {
                script {
                    sh "docker build -t amioss/app_petclinic:${env.BRANCH_NAME} ."
                    if ( env.BRANCH_NAME == 'master' ) {
                        containerVersion = getVersionFromContainer("amioss/app_petclinic:${env.BRANCH_NAME}")
                        failIfVersionExists("amioss","app_petclinic",containerVersion)
                        sh "docker build -t amioss/app_petclinic:${containerVersion} ."
                    }
                }
            }
        }
        stage('Run local Container') {
            agent any
            steps {
                sh 'docker rm -f petclinic-tomcat-temp || true'
                sh "docker run -d --network=bridge --name petclinic-tomcat-temp amioss/app_petclinic:${env.BRANCH_NAME} ./mvnw spring-boot:run -Dspring-boot.run.profiles=mysql"
            }
        }
        stage('Smoke-Test') {
            agent {
                docker {
                    image 'maven:3.5.0'
                    args '--network=bridge'
                }
            }
            steps {
                sh "cd regression-suite"
                sh "mvn clean -B test -DPETCLINIC_URL=http://petclinic-tomcat:8080/petclinic/"
            }
        }
        stage('Stop local container') {
            agent any
            steps {
                sh 'docker rm -f petclinic-tomcat-temp || true'
            }
        }
        stage('Push to dockerhub') {
            agent any
            steps {
                script {
                    if ( env.BRANCH_NAME == 'master' )
                        sh "docker push amioss/app_petclinic:${containerVersion}"
                    else sh "docker push amioss/app_petclinic:${env.BRANCH_NAME}"
                }
            }
        }
    }
    post {
        failure {
            slackSend (channel:"#petclinic", color: "CF1318", message: "${env.JOB_NAME} Failed (<${env.BUILD_URL}|Open>)")
        }
    }
}
