pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-nginx-image'
        CONTAINER_NAME = 'my-nginx-container'
        PORT = '9000'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-cred',
                    url: 'https://github.com/ravish142000/Basichtml.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d --name $CONTAINER_NAME -p $PORT:80 $DOCKER_IMAGE"
            }
        }

        stage('Verify Deployment') {
            steps {
                sh "curl http://localhost:$PORT"
            }
        }
    }

    post {
        always {
            sh 'docker stop $CONTAINER_NAME'
            sh 'docker rm $CONTAINER_NAME'
            sh 'docker rmi $DOCKER_IMAGE'
        }

        failure {
            mail to: 'your-email@example.com',
                 subject: 'Deployment Failed',
                 body: 'Deployment failed. Check Jenkins logs.'
        }
    }
}
