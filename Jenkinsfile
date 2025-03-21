pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'samimmondal/python-app:latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url:'https://github.com/abdulsamimmondal/python-docker-app.git',branch:'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
