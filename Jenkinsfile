pipeline {
  environment {
    registryCredential = 'dockerhub-registry'
    registry = 'eduarte/web-dvwa'
    dockerImage = ''
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
            DockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            DockerImage.push()
          }
        }
      }
    }
    stage('Anallyze image with Anchore'){
      steps {
        anchore name: registry
      }
    }
  }
}
