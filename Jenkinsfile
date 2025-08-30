pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/qiaoxingoh/p4.git'
            }
        }
        stage('Build') {
            steps {
                // Make gradlew executable and run it with ./
                sh 'chmod +x gradlew'
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                // Use sh for Linux, not bat
                sh './gradlew test'
            }
        }
        stage('Deploy') {
            steps {
                // Use sh for Linux, not powershell
                sh 'java -jar build/libs/hello-world-java-V1.jar'
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
        }
        failure {
            echo 'Build failed!'
        }
    }
}