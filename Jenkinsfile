pipeline {
    agent {
        docker {
            image 'maven:3.8.6-jdk-11'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nginx-image .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name my-nginx-container -p 9000:80 my-nginx-image'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl http://localhost:9000'
            }
        }
    }

    post {
        always {
            sh 'docker stop my-nginx-container'
            sh 'docker rm my-nginx-container'
            sh 'docker rmi my-nginx-image'
        }

        failure {
            mail to: 'your-email@example.com',
                 subject: 'Deployment Failed',
                 body: 'Deployment failed. Check Jenkins logs.'
        }
    }
}
