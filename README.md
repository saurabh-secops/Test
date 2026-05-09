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

You can use this repository in Jenkins to create a demo build pipeline. A sample Jenkinsfile could include:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t hello-world-app .'
            }
        }
    }
}
```

## Project Structure

- `src/main/java/com/example/HelloWorld.java` - Main application class
- `pom.xml` - Maven configuration
- `Dockerfile` - Docker build configuration