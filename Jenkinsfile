
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    appFrontend = docker.build("aminatug/bijouterie-frontend:${env.BUILD_NUMBER}", "./frontend")
                    appBackend  = docker.build("aminatug/bijouterie-backend:${env.BUILD_NUMBER}", "./backend")
                    appDb       = docker.build("aminatug/bijouterie-mysql:${env.BUILD_NUMBER}", "./database")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        appFrontend.push()
                        appBackend.push()
                        appDb.push()
                    }
                }
            }
        }
    }
}
