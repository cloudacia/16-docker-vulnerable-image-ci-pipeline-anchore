pipeline {
  environment {
    registryCredential = 'dockerhub-registry'
    repository = 'vulnerables/web-dvwa'
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
        sh 'docker --version'
        script {
          docker.withRegistry(registryCredential) {
            def image = docker.build(repository)
          }
        }
      }
    }
    stage('Analyze with Anchore plugin') {
      steps {
        writeFile file: 'anchore_images', text: imageLine
        anchore name: 'anchore_images'
      }
    }
    //stage('Build and push stable image to registry') {
    //  steps {
    //    script {
    //      docker.withRegistry('https://' + registry, registryCredential) {
    //        def image = docker.build(repository + ':prod')
    //        image.push()
    //      }
    //    }
    //  }
    //}
  }
}
