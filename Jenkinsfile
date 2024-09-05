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
        stage('Deploy') {
            steps {
                sshPublisher( publishers: [
                    sshPublisherDesc(
                        configName: 'Front-end-server',
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'dist/build-bench-ws/browser/**',
                                remoteDirectory: '', //Averiguar esto ahora
                                remoteDirectorySDF: false
                            )
                        ],
                        verbose: true,
                        
                    )
                ],
                alwaysPublishFromMaster: true
                )
            }
        }
    }
}