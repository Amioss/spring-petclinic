pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'spring-petclinic/src/test/jmeter/petclinic_test_plan.jmx'
            }
        }
}
}
