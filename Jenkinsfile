@Library ("shared") _
pipeline {
    agent { label 'slave' }
    environment {
    IMAGE_NAME = "docker-helloworld" 
                // provide the new docker image tag here which will be added to the docker image
}
    stages {
        stage('echo'){
            steps {
                script {
                    hello ()
                }
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                dockerbuild(IMAGE_NAME)

            }
        }
        stage('push') {
            steps {
                dockerpush(IMAGE_NAME)

            }
        }        

        stage('Deploy') {
            steps {
                dockerdeploy(IMAGE_NAME)
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        always {
            cleanWs()
        }
    }
}

