pipeline {
    agent any

    environment {
        IMAGE_NAME = 'tuusuario/toqueneldom'  // Cambia con tu nombre en Docker Hub
        DOCKER_CREDENTIALS_ID = 'docker'   // Usamos la credencial de Docker Hub
        GITHUB_CREDENTIALS_ID = 'Credencial-Git' // Aquí utilizamos la credencial de GitHub
        CONTAINER_NAME = 'toqueneldom'
        LOCAL_PORT = '8082'                         // El puerto en el que corre la app localmente
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: "${GITHUB_CREDENTIALS_ID}", url: 'https://github.com/Alexandracoder/toqueneldom.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Run Container Locally') {
            steps {
                sh '''
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d -p $LOCAL_PORT:80 --name $CONTAINER_NAME $IMAGE_NAME:latest
                '''
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    env.TAG = new Date().format("yyyyMMddHHmmss")
                    sh "docker tag $IMAGE_NAME:latest $IMAGE_NAME:$TAG"
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
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

