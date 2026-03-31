pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/VEDANTPANDEY35/meta-learning-stocks.git'
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
