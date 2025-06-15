pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t my-springboot-app .'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                  docker stop springboot || true
                  docker rm springboot || true
                  docker run -d --name springboot -p 8080:8080 my-springboot-app
                '''
            }
        }
    }
}