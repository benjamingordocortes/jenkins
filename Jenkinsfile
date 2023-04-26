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
      steps{
        script{
          withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ]) {
            bat "docker push benjamito/jenkinsprueba:latest"
          }
        }
      }
    }
  }
}
