pipeline {
  agent none

  parameters {
    string(name: 'IMAGE_NAME', defaultValue: 'alpinehelloworld', description: 'le nom de mon image docker')
    string(name: 'IMAGE_TAG', defaultValue: 'latest', description: 'le tag de mon image')
    string(name: 'DOCKERHUB_ID', defaultValue: 'franklinfoko', description: 'id docker hub')    
  }

  stages {
    
    stage ('Build de l\'image'){
      steps {
        sh 'docker build -t ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG} .'
      }
    }
    
    stage ('Delete old container'){
      steps {
        sh 'docker rm -f Webapp'
      }
    }
    
    stage ('Test Image'){
      steps {
        sh '''docker run -d -p 80:5000 -e PORT=5000 --name Webapp ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG}

              sleep 10

              curl http://3.235.196.58/
        '''
      }
    }

    stage ('Push image'){
      steps {
        withCredentials([gitUsernamePassword(credentialsId: 'hub-credentials', gitToolName: 'Default')]) {
            docker login -u ${DOCKERHUB_ID}
            docker push ${DOCKERHUB_ID}/${IMAGE_NAME}:${IMAGE_TAG}
          }
      }
    }
           
  }
}
