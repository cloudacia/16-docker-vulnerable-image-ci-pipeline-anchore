pipeline {
  environment {
    registryCredential = 'dockerhub-registry'
    repository = 'eduarte/web-dvwa'
    imageLine = 'dockerhub.com/eduarte/web-dvwa:lastest'
  }
  agent any
  stages {
    stage('Checkout SCM') {
      steps {
        checkout scm
      }
    }
    stage('Build image and push to registry') {
      steps {
        script {
          docker.withRegistry(registryCredential) {
            DockerImage = docker.build(repository)
          }
        }
      }
    }
    stage('Push image to registry') {
      steps {
        script {
          DockerImage.push()
        }
      }
    }
  }
}
