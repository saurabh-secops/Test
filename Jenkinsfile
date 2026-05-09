pipeline {
    agent any
    tools {
        maven 'Maven 3.9.6'  // Adjust to your Jenkins Maven installation
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t hello-world-app .'
            }
        }
    }
    post {
        always {
            echo 'Build completed'
        }
        failure {
            echo 'Build failed'
        }
    }
}