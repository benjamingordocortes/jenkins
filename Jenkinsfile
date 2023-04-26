pipeline {
  agent any

  stages{
    stage('docker build') {
      steps {
        script {
          sh "docker build -f Dockerfile -t benjamito/jenkinsprueba:latest ."
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