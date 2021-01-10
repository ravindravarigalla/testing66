pipeline {
  environment {
    registry = "trainingad1/ms-ref-service-a"
    registryCredential = 'dockerhub'
    dockerImage = 'docker'
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
  }
}

