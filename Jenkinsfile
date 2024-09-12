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
                        configName: 'front-prod',
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'dist/build-bench-ws/browser/**',
                                remoteDirectory: '', //Averiguar esto ahora
                                remoteDirectorySDF: false,
                                flatten: true
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