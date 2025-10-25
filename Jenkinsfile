@Library("Shared") _
pipeline {
    agent any
    stages {
        stage("Docker Hub Login & Pull Images") {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: "docker",   // Replace with your Jenkins credential ID
                        passwordVariable: "DOCKERHUB_PASSWORD",
                        usernameVariable: "DOCKERHUB_USERNAME"
                    )]) {
                        echo "Logging in to Docker Hub..."
                        sh "echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin"

                        echo "Pulling latest microservice images..."
                        sh "docker pull $DOCKERHUB_USERNAME/auth-service:latest"
                        sh "docker pull $DOCKERHUB_USERNAME/admin-service:latest"
                    }
                }
            }
        }

        stage("Deploy Services with Docker Compose") {
            steps {
                script {
                    echo "Deploying microservices using docker-compose..."
                    docker_compose()  // Calls your shared library function
                }
            }
        }
    }

    post {
        always {
            echo "Deployment finished."
        }
    }
}
