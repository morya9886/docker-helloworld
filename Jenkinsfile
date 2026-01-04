@Library ("shared") _
pipeline {
    agent { label 'slave' }

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
                dockerbuild('docker-helloworld')
                // give the new docker image tag here
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f helloworld || true
                  docker run -d --name helloworld -p 8081:8081 docker-helloworld
                '''
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

