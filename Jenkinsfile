pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Executing git checkout: Staging"
                sh 'ls'
            }

        }
        stage('Build - Staging Server') {
            steps {
                echo "Executing Build"
            }
        }
    }
}