pipeline {
    agent any
    environment {
        // Fixed spelling to 'environment'
        IMAGE_NAME = 'narendra2345/practice'
    }
    stages {
        stage('Checkout code') {
            steps {
                // Good job specifying the branch!
                git branch: 'main', url: 'https://github.com/Narendr12/devops12'
            }
        }
        stage('Building Docker image') {
            steps {
                // Use ${} for variables in 'sh'
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }
        stage('Pushing to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                    echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin
                    docker push ${IMAGE_NAME}:latest
                    docker logout
                    """
                }
            }
        }
    }
}
