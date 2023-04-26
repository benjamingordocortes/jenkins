pipeline {
  agent any
  
  environment {
    DOCKER_HUB_REGISTRY = "docker.io"
    DOCKER_HUB_REPO = "benjamito"
    DOCKER_HUB_CREDENTIALS = credentials("docker-hub-credentials")
    DOCKER_IMAGE_NAME = "${DOCKER_HUB_REPO}/jenkinsprueba"
    DOCKER_IMAGE_TAG = "latest"
  }
  
  stages {
    stage("Build Docker image") {
      steps {
        script {
          docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", ".")
        }
      }
    }
    
    stage("Push Docker image") {
      steps {
        script {
          docker.withRegistry('', "${DOCKER_HUB_CREDENTIALS}") {
            docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
          }
        }
      }
    }
  }
}