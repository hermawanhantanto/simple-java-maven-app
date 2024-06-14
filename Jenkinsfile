node {
    docker.image('maven:3.9.0').inside('-v /root/.m2:/root/.m2') {
        stage('Build') {
            try {
                sh 'mvn -B -DskipTests clean package'
            } catch (Exception e) {
                error "Build failed: ${e.message}"
            }
        }
        
        stage('Test') {
            try {
                sh 'mvn test'
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
        
        stage('Deliver') {
            try {
                sh './jenkins/scripts/deliver.sh'
            } catch (Exception e) {
                error "Delivery failed: ${e.message}"
            }
        }
    }
}

