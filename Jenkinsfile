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
    stage('Push image') {
      withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ]) {
      bat "docker push devopsglobalmedia/teamcitydocker:build"
      }
    }
  }
}
