pipeline {
  environment {
    registryCredential = 'dockerhub-registry'
    repository = 'eduarte/web-dvwa'    
  }
  agent any
  stages {
    stage('Checkout SCM') {
      steps {
        checkout scm
      }
    }
    stage('Build image') {
      steps {
        script {
            DockerImage = docker.build(repository)
        }
      }
    }
    stage('Push image') {
      steps {
        script {
          docker.WithRegistry('', registryCredential) {
            DockerImage.push()
          }
        }
      }
    }
  }
}
