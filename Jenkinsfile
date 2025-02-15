pipeline {
  agent any

  parameters {
    string(name: 'CONTAINER_NAME', defaultValue: 'alpine', description: 'the name of my container')
    string(name: 'IMAGE_NAME', defaultValue: 'alpine_image', description: 'the name of my container image')
    string(name: 'IMAGE_TAG', defaultValue: '1.2', description: 'The version of my image')
  }

  stages {
    stage('Build docker image') {
      steps {
        sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
        sh 'docker rm -f ${CONTAINER_NAME}'
      }
    }
  }
}