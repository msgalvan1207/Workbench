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
                sh 'ng build'
            }
        }
        stage('Serve') {
            steps {
                sh 'cp -a dist/build-bench-ws/browser/. /var/www/html'
            }
        }
    }
}