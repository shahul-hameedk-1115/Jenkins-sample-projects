# 🖥️ Full-Stack Java (Maven) + Node.js App with MySQL and Jenkins Pipeline 🚀

### Author - @Shahul Hameed K (https://www.linkedin.com/in/hameed15/)


#### This project demonstrates a full-stack application using Java (Maven) for the backend, Node.js for the frontend, MySQL as the database, and Jenkins for continuous integration and delivery (CI/CD). 🤖🔧

Follow this step-by-step guide to set up the project. 📚


### Prerequisites

Docker installed on your machine.

Jenkins for setting up the CI/CD pipeline.

GitHub account and repository for version control.

#### Step 1: Create Folder Structure

First, create the folder structure for the backend, frontend, and MySQL setup. You can create the directories manually or use the following commands:

```mkdir fullstack-app
cd fullstack-app
mkdir backend-java-app frontend-node-app mysql
Here’s how the structure will look:

fullstack-app/
├── backend-java-app/
├── frontend-node-app/
└── mysql/
```

1. backend-java-app/
This folder will contain the Java backend code, Maven configuration, and Docker setup.

2. frontend-node-app/
This folder will contain the Node.js frontend code.

3. mysql/
This folder will contain the MySQL database setup, initialization scripts, and configuration.

#### Step 2: Initialize Git and Create GitHub Repository

Initialize a Git repository inside the project folder:
```git init```

Create a GitHub repository and link it to the local project:
```git remote add origin https://github.com/your-username/fullstack-app.git```
#### Step 3: Set Up the Backend (Java)

Navigate to the backend folder:

```cd backend-java-app```

Create a basic Maven pom.xml file to manage Java dependencies:
```<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>

<groupId>com.example</groupId>
<artifactId>backend-java-app</artifactId>
<version>1.0-SNAPSHOT</version>
</project>
Create a basic Java application. For example, App.java:
public class App {
public static void main(String[] args) {
System.out.println("Hello, world!");
    }
}
```
#### Step 4: Set Up the Frontend (Node.js)

Navigate to the frontend folder:
```cd ../frontend-node-app```
Initialize a Node.js project:
```npm init -y```
Install dependencies:
```npm install express```
Create a basic app.js file for the frontend:
```const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello from the frontend!');
});

app.listen(3000, () => {
    console.log('Frontend app running on port 3000');
});
```
#### Step 5: Set Up MySQL

Navigate to the MySQL folder:
```cd ../mysql```
Create a docker-compose.yml file to configure the MySQL container:
```version: '3'
services:
  mysql-db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: myappdb
    ports:
      - "3306:3306"
Start MySQL container:
docker-compose up -d
```
#### Step 6: Set Up Docker

Create a Dockerfile for the Java backend inside backend-java-app:
```FROM openjdk:11-jdk
WORKDIR /app
COPY . .
RUN javac App.java
CMD ["java", "App"]
```
Create a Dockerfile for the Node.js frontend inside frontend-node-app:
```FROM node:14
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "app.js"]
```
Build the Docker images for both services:
```docker build -t backend-java-app ./backend-java-app```
```docker build -t frontend-node-app ./frontend-node-app```
Run both containers:
```docker run -d -p 8080:8080 backend-java-app```
```docker run -d -p 3000:3000 frontend-node-app```
#### Step 7: Set Up Jenkins Pipeline

Create a Jenkinsfile in the root directory of the project:
```
pipeline {
    agent any
    stages {
        stage('Build Backend') {
            steps {
                script {
                    docker.build("backend-java-app", "./backend-java-app")
                }
            }
        }
        stage('Build Frontend') {
            steps {
                script {
                    docker.build("frontend-node-app", "./frontend-node-app")
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Add deployment logic, e.g., push to Docker Hub, deploy to Kubernetes, etc.
                }
            }
        }
    }
}
```
#### Step 8: Running the Full Stack App

Run the application with Docker Compose:
In the root folder of your project, create a ```docker-compose.yml``` file to orchestrate both backend and frontend containers.
```
version: '3'
services:
  mysql-db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: myappdb
    ports:
      - "3306:3306"

  backend:
    build: ./backend-java-app
    ports:
      - "8080:8080"
    depends_on:
      - mysql-db

  frontend:
    build: ./frontend-node-app
    ports:
      - "3000:3000"
    depends_on:
      - backend
```
Start everything using Docker Compose:
```docker-compose up --build```
This will build and start the containers for MySQL, backend, and frontend.
#### Step 9: Final Notes

Once everything is up and running:

Frontend: Accessible at ```http://localhost:3000```

Backend: Accessible at ```http://localhost:8080```

MySQL: Accessible at ```localhost:3306```

You can further expand this setup with additional features, such as authentication, advanced database operations, and more sophisticated deployment strategies.

## Feel free to contribute to the project by forking it, submitting issues, or making pull requests.

