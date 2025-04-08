pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests (placeholder)'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop my-app || true'
                sh 'docker rm my-app || true'
                sh 'docker run -d --name my-app -p 3000:3000 my-app:latest'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}