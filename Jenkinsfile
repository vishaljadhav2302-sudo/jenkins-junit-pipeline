pipeline {
    agent any
    stages {
        stage('1. Checkout Code') {
            steps { echo 'Code checked out from GitHub.' }
        }
        stage('2. Build & Run JUnit Tests') {
            steps { sh 'mvn clean test' }
            post {
                always { junit '**/target/surefire-reports/*.xml' }
            }
        }
        stage('3. Package Application') {
            steps { sh 'mvn package -DskipTests' }
        }
        stage('4. Deploy Application') {
            steps {
                sh '''
                    mkdir -p /tmp/deployed-app
                    cp target/calculator-app-1.0-SNAPSHOT.jar /tmp/deployed-app/
                    java -jar /tmp/deployed-app/calculator-app-1.0-SNAPSHOT.jar
                '''
            }
        }
    }
}
