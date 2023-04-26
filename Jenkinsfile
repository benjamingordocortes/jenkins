pipeline {
  agent any

  stages{
    stage('docker build') {
      steps {
        script {
          sh "docker build -f Dockerfile -t benjamito/nginxpage:latest"
        }
      }
    }
    stage('docker push') {
      steps {
        script {
          sh "docker push benjamito/nginxpage:latest"
        }
      }
    }
  }
}