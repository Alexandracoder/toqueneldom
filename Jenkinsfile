pipeline {
    agent any

    environment {
        IMAGE_NAME = 'alexandracoder'  // Cambia con tu nombre en Docker Hub
        DOCKER_CREDENTIALS_ID = 'docker'     // Usamos la credencial de Docker Hub
        GITHUB_CREDENTIALS_ID = 'Credencial-Git' // Usamos la credencial de GitHub
        CONTAINER_NAME = 'toqueneldom'
        LOCAL_PORT = '8082'                         // El puerto en el que corre la app localmente
    }

    stages {
        stage('Checkout') {
            steps {
                // Cambia a la rama correcta 'main' en lugar de 'master'
                git credentialsId: "${GITHUB_CREDENTIALS_ID}", branch: 'main', url: 'https://github.com/Alexandracoder/toqueneldom.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Construyendo imagen Docker..."
                    // Construye la imagen de Docker
                    sh 'docker build -t $IMAGE_NAME:latest .'
                }
            }
        }

        stage('Run Container Locally') {
            steps {
                script {
                    echo "Ejecutando el contenedor localmente en el puerto $LOCAL_PORT..."
                    // Elimina el contenedor si ya está corriendo
                    sh '''
                        docker rm -f $CONTAINER_NAME || true
                        docker run -d -p $LOCAL_PORT:80 --name $CONTAINER_NAME $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    echo "Etiquetando la imagen Docker con un nuevo tag..."
                    env.TAG = new Date().format("yyyyMMddHHmmss")  // Usando la fecha y hora como tag
                    // Etiqueta la imagen Docker
                    sh "docker tag $IMAGE_NAME:latest $IMAGE_NAME:$TAG"
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
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
