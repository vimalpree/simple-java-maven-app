pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts 'target/*.jar'
            }
        }
    }
    post {
        success { echo 'SUCCESS ✅' }
    }
}
