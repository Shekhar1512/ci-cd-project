pipeline {

    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Shekhar1512/ci-cd-project.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t my-static-image .'
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

    }

}
