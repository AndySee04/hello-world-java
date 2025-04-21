pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/AndySee04/hello-world-java.git'
            }
        }
        stage('Build') {
            steps {
                powershell 'gradle build'
                // bat 'gradle build'
            }
        }
        stage('Test') {
            steps {
                powershell 'gradle test'
                // bat 'gradle test'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    powershell '''
                        $jarPath = "build/libs/hello-world-java-1.0-SNAPSHOT.jar"
                        if (Test-Path $jarPath) {
                            java -jar $jarPath
                        } else {
                            Write-Error "JAR file not found at: $jarPath"
                            exit 1
                        }
                    '''
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir() // Clean up the workspace after the build
        }
        success {
            echo 'Build succeeded!!!'
            // You could add notification steps here
        }
        failure {
            echo 'Build failed!'
            // You could add notification steps here
        }
    }
}
