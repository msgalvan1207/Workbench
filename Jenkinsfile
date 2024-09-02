pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Executing git checkout: Staging"
                sh 'node --version'
                sh 'npm --version'
                sh 'ng version'
            }

        }
        stage('Build - Staging Server') {
            steps {
                echo "Executing Build"
            }
        }
    }
}