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
                // Debug: see what files exist
                sh 'ls -la'
                
                // Debug: see if gradlew is there
                sh 'ls -la gradlew'
                
                // Make it executable
                sh 'chmod +x gradlew'
                
                // Debug: check permissions after chmod
                sh 'ls -la gradlew'
                
                // Now run it with ./
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'  // 🔥 MUST have ./ prefix!
            }
        }
        stage('Deploy') {
            steps {
                sh 'java -jar build/libs/hello-world-java-V1.jar'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace'
            deleteDir()
        }
        success {
            echo 'Build succeeded!!!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}