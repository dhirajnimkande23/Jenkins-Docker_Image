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
                    echo 'Docker Image build successfull'
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
