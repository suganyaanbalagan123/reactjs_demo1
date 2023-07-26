pipeline {
    agent any

    // Define environment variables (update these with your credentials)
    environment {
        DOCKER_HUB_USERNAME = 'suganyamadhan1996'
        DOCKER_HUB_PASSWORD = credentials('567') // Jenkins credential ID for Docker Hub password
        DOCKER_HUB_REPO = 'suganyamadhan1996/dev'
        IMAGE_TAG = "${env.BUILD_NUMBER}" // Using Jenkins build number as the Docker image tag
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub "dev" branch
                git branch: 'dev', url: 'https://github.com/suganyaanbalagan123/reactjs-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    // Build the Docker image without sudo
                    sh "docker build -t ${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPO}:${IMAGE_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Push the Docker image to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '567') {
                        docker.image("${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPO}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
