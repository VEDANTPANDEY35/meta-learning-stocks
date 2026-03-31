pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("meta-learning")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image("meta-learning").run("-p 8888:8888")
                }
            }
        }

    }
}
