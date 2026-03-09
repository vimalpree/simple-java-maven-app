pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                script {
                    // Find the directory containing pom.xml (handles subdir checkout)
                    def pomDir = findFiles(glob: '**/pom.xml')[0]?.path ?: 'pom.xml'
                    def projectDir = pomDir.substring(0, pomDir.lastIndexOf('/'))
                    
                    dir(projectDir) {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                script {
                    // Archive from the project dir too
                    def pomDir = findFiles(glob: '**/pom.xml')[0]?.path ?: 'pom.xml'
                    def projectDir = pomDir.substring(0, pomDir.lastIndexOf('/'))
                    archiveArtifacts artifacts: "${projectDir}/target/*.jar", allowEmptyArchive: true
                }
            }
        }
    }

    post {
        success {
            echo '✅Build succeeded 🎉'
        }
        failure {
            echo 'Build failed ❌ - check pom.xml location and Maven setup'
        }
    }
}
