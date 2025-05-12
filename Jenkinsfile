pipeline {
    agent any

    environment {
        IMAGE_NAME = 'alexandracoder'
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds'
        GITHUB_CREDENTIALS_ID = 'Credencial-Git'
        CONTAINER_NAME = 'toqueneldom'
        LOCAL_PORT = '8082'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: "${GITHUB_CREDENTIALS_ID}", url: 'https://github.com/tuusuario/toqueneldom.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Run Container Locally') {
            steps {
                sh """
                    docker rm -f $CONTAINER_NAME || true
                    docker run -d -p $LOCAL_PORT:80 --name $CONTAINER_NAME $IMAGE_NAME:latest
                """
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    TAG = new Date().format("yyyyMMddHHmmss")
                    env.TAG = TAG
                    sh "docker tag $IMAGE_NAME:latest $IMAGE_NAME:$TAG"
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
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
