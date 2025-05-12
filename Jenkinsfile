pipeline {
    agent any

    environment {
        IMAGE_NAME = 'alexandracoder/alexandracoder-pipeline'  // Repositorio en Docker Hub
        TAG = '20250512133511'  // Tag de la imagen, puede ser el timestamp o la versión
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

        stage('Run Container Locally') {
            steps {
                script {
                    echo "Ejecutando el contenedor localmente en el puerto 8082..."
                    sh '''
                        docker rm -f toqueneldom || true
                        docker run -d -p 8082:80 --name toqueneldom $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    echo "Etiquetando la imagen Docker con un nuevo tag..."
                    sh 'docker tag $IMAGE_NAME:latest $IMAGE_NAME:$TAG'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS_ID', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        echo "Pusheando la imagen a Docker Hub..."
                        // Inicia sesión en Docker Hub
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
