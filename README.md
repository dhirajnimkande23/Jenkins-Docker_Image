🐳 Jenkins Pipeline for Python Hello World (Docker)

This repository contains a Jenkins Declarative Pipeline (Jenkinsfile) that automates the process of building, running, and pushing a Docker image for a simple Python application.

🚀 Pipeline Overview

The pipeline performs the following key steps:

Clone Repo – Pulls the latest code from the GitHub repository.

Build Docker Image – Builds a Docker image using the provided Dockerfile.

Run Container – Runs the container to verify it builds and runs successfully.

Push to Docker Hub – Tags and pushes the built image to Docker Hub.

🧩 Jenkinsfile Explanation
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'python-hello-world'
        DOCKER_TAG = 'latest'
        DOCKER_HUB_REPO = 'dhiraj23/python-hello-world'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/dhirajnimkande23/pythonhelloworld.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('python-hello-world')
                    echo 'Docker Image build successful'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    dockerImage.run()
                    echo 'Container created'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                        sh 'docker tag python-hello-world dhiraj23/python-hello-world:latest'
                        sh 'docker push dhiraj23/python-hello-world:latest'
                        echo 'Docker image pushed to Docker Hub successfully'
                    }
                }
            }
        }
    }
}

🏗️ How It Works
Stage	Description
Clone Repo	Clones the Python Hello World repository from GitHub.
Build Docker Image	Uses the Dockerfile to create an image named python-hello-world.
Run Container	Starts a container to ensure the image works as expected.
Push to Docker Hub	Tags and pushes the image to the Docker Hub repository dhiraj23/python-hello-world.
⚙️ Prerequisites

Before running this pipeline, ensure:

Jenkins is installed and configured.

Jenkins has Docker and Git installed.

A Jenkins credential named dockerhub-creds is created with your Docker Hub username and password.

The Jenkins agent has permission to build and push Docker images.

🧾 Docker Hub Repository

The built image will be available at:
👉 dhiraj23/python-hello-world

🧠 Notes

Update the repository URL in the pipeline if the project name changes.

To customize the tag, modify the DOCKER_TAG environment variable.

🖋️ Author

👤 Dhiraj Nimkande

📦 Docker Hub: dhiraj23

💻 GitHub: @dhirajnimkande23

You can add testing or linting stages before building the Docker image for better CI/CD practice.# Jenkins-Docker_Image
Create Docker image by using Jenkins Pipeline

