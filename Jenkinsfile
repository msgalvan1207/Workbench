pipeline {
    agent none
    stages {
        stage('Checkout - Staging Server') {
            agent {label 'Agent1'}
            steps {
                echo "Executing git checkout: Staging"
            }

        }
        stage('Build - Staging Server') {
            agent {label 'Agent1'}
            steps {
                echo "Executing Build"
            }

        }
        stage('Testing - Staging Server') {
            agent {label 'Agent1'}
            steps {
                echo "Running Tests"
            }

        }
        stage('Static Analysis - Staging Server') {
            agent {label 'Agent1'}
            steps {
                echo "Running Static analysys"
            }

        }
    }
}