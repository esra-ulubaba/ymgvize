pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        IMAGE_NAME = "ymg-vize"
        CONTAINER_NAME = "nginx-container"
    }

    stages {
        stage('Repository Klonla') {
            steps {
                git url: 'https://github.com/esra-ulubaba/ymgvize.git/', branch: 'main'
            }
        }

        stage('Docker Image Olustur') {
            steps {
                echo "Docker Image olusturuluyor..."
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Eski Container Durduruluyor') {
            steps {
                echo "Eski container durduruluyor..."
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }

        stage('Yeni Container Olusturuluyor') {
            steps {
                echo "Yeni container olusturuluyor..."
                sh "docker run -d --name ${CONTAINER_NAME} -p 5050:80 ${IMAGE_NAME}"
            }
        }
    }

    post {
        success {
            echo "Yayin basarili: http://localhost:5050"
        }
        failure {
            echo "Pipeline basarisiz oldu"
        }
    }
}
