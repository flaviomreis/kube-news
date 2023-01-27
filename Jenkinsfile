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
    // stage ('push docker image') {
    //   steps {
    //     script {
    //       docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
    //         dockerapp.push('latest')
    //         dockerapp.push("${env.BUILD_ID}")
    //     }
    //   }
    // }
    stage ('deploy kubernetes') {
      steps {
        withKubeConfig ([credentialsId: 'kubeconfig']) {
          sh 'kubectl apply -f ./k8s/postgres/service.yaml'
          sh 'kubectl apply -f ./k8s/postgres/deployment.yaml'
        }
      }
    }
  }
}
