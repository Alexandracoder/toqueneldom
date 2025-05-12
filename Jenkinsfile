pipeline {
    agent any
    environment {
        IMAGE_NAME = 'alexandracoder/alexandracoder-pipeline'
        TAG = "20250512133511"
        DOCKER_CREDENTIALS_ID = 'docker' // Asegúrate de usar el ID correcto aquí
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Construyendo imagen Docker..."
                    sh 'docker build -t $IMAGE_NAME:latest .'
                }
            }
        }
        stage('Tag Docker Image') {
            steps {
                script {
                    echo "Etiquetando la imagen Docker..."
                    sh "docker tag $IMAGE_NAME:latest $IMAGE_NAME:$TAG"
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        echo "Pusheando la imagen a Docker Hub..."
                        sh '''
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push $IMAGE_NAME:latest
                            docker push $IMAGE_NAME:$TAG
                            docker logout
                        '''
                    }
                }
            }
        }
    }
}

