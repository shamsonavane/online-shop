pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('docker-hub-credentials-id') // Docker Hub credentials stored in Jenkins
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                        sudo apt-get update
                        sudo apt-get install -y docker docker-compose
                        '''
                    } else {
                        echo 'Ensure Docker is installed on the Windows node.'
                    }
                }
            }
        }
        
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

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker login -u "${DOCKER_CREDENTIALS_USR}" -p "${DOCKER_CREDENTIALS_PSW}" docker.io'
                        sh 'docker tag your_image_name upasanatestdocker/job1_web2.0'
                        sh 'docker push upasanatestdocker/job1_web2.0'
                    } else {
                        bat 'docker login -u "${DOCKER_CREDENTIALS_USR}" -p "${DOCKER_CREDENTIALS_PSW}" docker.io'
                        bat 'docker tag your_image_name upasanatestdocker/job1_web2.0'
                        bat 'docker push upasanatestdocker/job1_web2.0'
                    }
                }
            }
        }
    }
}

