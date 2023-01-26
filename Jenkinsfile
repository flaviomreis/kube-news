pipeline {
  agent any
  stages {
    stage ('build docker image') {
      steps {
        script {
          dockerapp = docker.build("f18s.f9s/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
        }
      }
    }
  }
}