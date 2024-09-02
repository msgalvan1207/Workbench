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
        stage('Build') {
            steps {
                echo "Executing Build"
                sh 'npm install'
                sh 'ng build'
            }
        }
        stage('Serve') {
            steps {
                echo "Starting web server"
                echo "This should be changed to nginx or apache or smth later"
                sh 'ng s'
            }
        }
    }
}