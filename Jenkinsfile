pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    environment {
        GIT_REPO = 'Workbench'
        GIT_CREDENTIAL_ID = 'github-auth-token'
    }

    parameters {
        choice(name: 'BUILD', choices: ['production', 'development'], description: 'type of build and server')
    }

    stages {

        stage('Checkout') {
            steps {
                //scmSkip(deleteBuild: true, skipPattern:'.*\\[ci-skip\\].*')
                git branch : 'main',
                    credentialsId: env.GIT_CREDENTIAL_ID,
                    url: 'https://github.com/msgalvan1207/' + env.GIT_REPO
            }
        }


        stage('Check') {
            steps {
                echo "Executing git checkout: Staging"
                sh 'node --version'
                sh 'npm --version'
                sh 'ng version'
                echo "Building for the following environment: ${params.BUILD}"
            }

        }
        stage('Build') {
            steps {
                echo "Executing Build"
                sh 'npm install'
                sh "ng build --configuration ${params.BUILD}"
            }
        }
        stage('Deploy') {
            steps {


                script {
                    def deployConfigName
                    if (params.BUILD == 'production') {
                        deployConfigName = 'front-prod'
                    } else if {params.BUILD == 'development'}{
                        deployConfigName = 'front-qa'
                    } else {
                        error "Unsuported build type: ${params.BUILD}"
                    }
                }





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
    post {
        always {
            cleanWs()
            deleteDir()
            dir("${env.GIT_REPO}@tmp") {
                deleteDir()
            }
        }
    }
}