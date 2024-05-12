pipeline {
  agent any
  environment {
      registry = "docker.io"
      registryCredential = 'dockerhub'
      SERVICE = 'backend'
  }
  stages {

    stage('build') {
      steps {
        sh "docker build -t $SERVICE ."
          sh "docker tag $SERVICE $registry/$SERVICE"
          sh "docker login -u $registryUsername -p $registryPassword"
          sh "docker push $registry/$SERVICE"
          sh "helm upgrade --install $SERVICE ./helm-chart --set image=$registry/$SERVICE"
      }
    }
  }
}
