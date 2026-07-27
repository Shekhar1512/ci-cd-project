pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build --no-cache \
                -t my-static-image .
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop my-static-container || true

                docker rm my-static-container || true

                docker run -d \
                --name my-static-container \
                -p 80:80 \
                my-static-image
                '''
            }
        }

        stage('Cleanup') {
            steps {
                sh '''
                docker image prune -f
                '''
            }
        }

    }

}
