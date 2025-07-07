pipeline {
  agent any

  environment {
    REGISTRY = 'docker.io'
    REPO     = 'wlals2/company-infra-finish' // DockerHub 아이디/레포 맞게 수정!
    IMAGE    = "${REPO}:${BUILD_NUMBER}"
    // DOCKERHUB_CREDENTIALS는 Jenkins에 등록해둘 것!
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          sh 'docker build -t $IMAGE .'
        }
      }
    }
    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_CREDENTIALS', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh '''
            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin $REGISTRY
            docker push $IMAGE
            docker logout $REGISTRY
          '''
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}

