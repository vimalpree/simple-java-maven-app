pipeline {
    agent any
    
    tools {
        maven 'Maven3'  // matches the name from Global Tool Config
        jdk 'java-17-openjdk'  // or whatever JDK name you set
    }

    stages {
        stage('Debug') {
            steps {
                sh 'ls -la'
                sh 'pwd'
                sh 'mvn --version || echo "Maven not in PATH yet"'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        success { echo '🎉 SUCCESS - check Artifacts tab!' }
        failure { echo '💥 FAILED - see logs above' }
    }
}
