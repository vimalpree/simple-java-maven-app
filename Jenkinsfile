pipeline {
    agent any

    stages {
        stage('01 - Debug') {
            steps {
                sh '''
                    echo "=== Ready to build ==="
                    ls -la | grep pom
                    mvn --version
                    pwd
                '''
            }
        }
        
        stage('02 - Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('03 - Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        success { echo '✅ SUCCESS! JAR archived.' }
        failure { echo '❌ FAILED.' }
    }
}
