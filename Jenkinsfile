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
                // FIRST make it executable, THEN run it with ./
                sh 'chmod +x gradlew'
                sh './gradlew build'  // 🔥 MUST have ./ prefix!
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