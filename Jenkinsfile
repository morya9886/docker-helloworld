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
                sh 'docker build -t docker-helloworld .'
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

