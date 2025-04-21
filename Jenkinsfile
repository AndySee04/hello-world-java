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
                // powershell 'gradle clean build'
                bat 'start gradlew build'
            }
        }
        stage('Test') {
            steps {
                // powershell 'gradle test'
                bat 'start gradlew test'
            }
        }
        stage('Deploy') {
            steps {
                powershell 'java -jar build/libs/hello-world-javaV1.jar'
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
