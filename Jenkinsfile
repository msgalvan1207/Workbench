pipeline {
    agent any
    stages {
        stage('Check') {
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
                sh 'ng build --output-path /var/www/html'
            }
        }
        stage('Serve') {
            steps {
                echo "xd"
            }
        }
    }
}