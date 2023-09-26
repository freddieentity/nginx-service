pipeline {
    agent any

    environment {
        CONTAINER_REGISTRY= "docker.io"
        CONTAINER_REPOSITORY= "freddieentity"
        APPLICATION_SOURCE_URL = 'https://github.com/freddieentity/nginx-service.git'
        APPLICATION_NAME = "nginx-service"
        CONTAINER_BUILD_CONTEXT = "."
    }
    stages {
        stage('UnitTest') {
            steps {
                echo 'UnitTesting..'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                sh "echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin"
                sh "docker build -t ${CONTAINER_REGISTRY}/${CONTAINER_REPOSITORY}/${APPLICATION_NAME}:dev ${CONTAINER_BUILD_CONTEXT}"
                sh "docker push ${CONTAINER_REGISTRY}/${CONTAINER_REPOSITORY}/${APPLICATION_NAME}:dev"
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying to DEV....'
            }
        }
    }
    post { 
        always { 
            cleanWs()
        }
    }
}
