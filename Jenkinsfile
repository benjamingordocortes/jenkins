pipeline {
  environment {
    registry = "benjamito/jenkinsprueba"
    registryCredential = 'docker-hub-credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Contruyendo imagen') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    stage('Subiendo imagen a repositorio') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy de imagen') {
      steps{
        script{
          withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: 'https://192.168.0.100:34689']) {
            sh 'kubectl apply -f deploy.yaml'
          }
        }
      }
    }
  }
} 