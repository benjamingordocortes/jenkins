pipeline {
  environment {
    registry = "benjamito/jenkinsprueba"
    registryCredential = 'docker-hub-credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    stage('Apply Kubernetes files') {
      steps{
        script{
          withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: 'https://192.168.0.32:61310']) {
            sh 'kubectl apply -f deploy.yaml'
          }
        }
      }
    }
  }
} 