pipeline {
    agent any
    stages {
        stage('SCM Checkout') {
            steps {
                git credentialsId: '4cc785e9-441d-4818-a248-2bfb2148004d', url: 'https://github.com/VardhanNS/phpmysql-app.git'
            }
        }

        stage('Run Docker Compose File') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker-compose build'
                        sh 'docker-compose up -d'
                    } else {
                        bat 'docker-compose build'
                        bat 'docker-compose up -d'
                    }
                }
            }
        }

        stage('PUSH image to Docker Hub') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker login -u "upasanatestdocker" -p "Zephyr@17" docker.io'
                        sh 'docker push upasanatestdocker/job1_web2.0'
                    } else {
                        bat 'docker login -u "upasanatestdocker" -p "Zephyr@17" docker.io'
                        bat 'docker push upasanatestdocker/job1_web2.0'
                    }
                }
            }
        }
    }
}
