pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests configured"'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t angular-seed-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop angular-app || true
                docker rm angular-app || true
                docker run -d -p 4200:80 --name angular-app angular-seed-app
                '''
            }
        }
    }
}
