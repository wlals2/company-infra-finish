pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
    - name: docker
      image: docker:24.0.2-dind
      command:
        - cat
      tty: true
      volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
  volumes:
    - name: docker-sock
      hostPath:
        path: /var/run/docker.sock
        type: Socket
"""
      defaultContainer 'docker'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker version'
        sh 'docker build -t wlals2/company-infra-finish:$BUILD_NUMBER .'
      }
    }
    stage('Push Docker Image') {
      steps {
        echo 'Push Docker Image 단계 - 임시 실행'
        // 실제 push 명령은 이후 추가
      }
    }
  }
}

