# Multi-stage-multi-agent
# Jenkins CI Pipeline — Node.js + React + Maven with Docker Agents

This project contains a simple Jenkins pipeline that demonstrates how to set up a Continuous Integration (CI) process using Jenkins with Docker-based agents for both back-end and front-end environments.

---

## 🛠️ What This Pipeline Does

The pipeline runs in **two stages**, each using a different Docker container:

### 🔧 Stage 1: Back-end
- Uses the `maven:3.8.1-adoptopenjdk-11` Docker image.
- Checks Maven installation by printing the Maven version.

### 🎨 Stage 2: Front-end
- Uses the `node:16-alpine` Docker image.
- Verifies Node.js and npm are installed.
- Installs React CLI globally via `create-react-app`.
- Verifies the `create-react-app` installation.

---

## 💡 Purpose

This pipeline serves as a basic template to:
- Learn how to use **Jenkins pipelines with Docker agents**.
- Understand environment verification for **Java/Maven** and **Node/React** projects.
- Lay the groundwork for future CI/CD setups.

---

## 🐳 Technologies Used

| Component   | Description                                 |
|-------------|---------------------------------------------|
| Jenkins     | CI/CD automation server                     |
| Docker      | Container platform to isolate environments |
| Maven       | Java project management and build tool     |
| Node.js     | JavaScript runtime for the front-end       |
| React       | JavaScript library (via `create-react-app`)|

---

## 📁 Jenkinsfile Structure

```groovy
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh '''
          node --version
          npm --version
          npm install -g create-react-app
          create-react-app --version
        '''
      }
    }
  }
}
