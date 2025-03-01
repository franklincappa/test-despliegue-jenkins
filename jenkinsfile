pipeline {
    agent any

    environment {
        IMAGE_NAME = "mi-app-docker"
        CONTAINER_NAME = "mi-app-container"
        GIT_REPO = "https://github.com/franklincappa/test-despliegue-jenkins.git"
        GIT_BRANCH = "master"
    }

    stages {
        stage('Clonar Código') {
            steps {
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Detener Contenedor Anterior') {
            steps {
                script {
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Desplegar Nuevo Contenedor') {
            steps {
                sh "docker run -d --name ${CONTAINER_NAME} -p 5000:5000 ${IMAGE_NAME}"
            }
        }

        stage('Verificar Despliegue') {
            steps {
                sh "docker ps -a"
            }
        }
    }
}
