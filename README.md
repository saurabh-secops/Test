# Java Hello World App

A simple Java application that prints "Hello, World!" to demonstrate building with Maven and Docker for Jenkins CI/CD.

## Prerequisites

- Java 11 or higher
- Maven 3.6 or higher
- Docker

## Building and Running Locally

### With Maven

```bash
mvn clean compile
mvn exec:java
```

### With Docker

```bash
docker build -t hello-world-app .
docker run hello-world-app
```

## Jenkins Pipeline

This repository includes a `Jenkinsfile` for a demo build pipeline. Make sure Jenkins has Maven and Docker configured.

If you encounter plugin resolution errors, ensure Maven is properly configured in Jenkins with access to Maven Central repository. You may need to configure proxy settings if behind a firewall.

The included Jenkinsfile uses:

```groovy
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
```

## Project Structure

- `src/main/java/com/example/HelloWorld.java` - Main application class
- `pom.xml` - Maven configuration
- `Dockerfile` - Docker build configuration