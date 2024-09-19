pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    environment {
        GIT_REPO = 'Workbench'
        GIT_CREDENTIAL_ID = 'github-auth-token'
        DEPLOY_CONFIG_NAME = ''
        
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
                    def deployServer = (params.BUILD=='production') ? 'prod': 'qa'

                    sh 'for file in dist/build-bench-ws/browser/* ; do filename=$(basename "$file"); curl -k -F "$filename=@$file" https://host.docker.internal:5000/upload/${deployServer}/front; done'
                    sh 'curl -k https://host.docker.internal:5000/deploy/${deployServer}/front'
                }
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