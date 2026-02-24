pipeline {
    agent any

    environment {
        IMAGE_NAME = "demo-jenkins-app"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'file:///home/edi/demo-jenkins'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f demo-container || true
                docker run -d -p 3001:3000 --name demo-container $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminat cu succes!'
        }
        failure {
            echo 'Pipeline a esuat!'
        }
    }
}
