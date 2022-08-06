pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('gsiddharth276-dockerhub')
  }
  stages {
    
    stage('Greeting') {
      steps {
        sh 'echo Hi, Welcome to Jenkins and Dockerhub Integration'
      }
    }
    
    stage('Build') {
      steps {
        sh 'docker build -t gsiddharth276/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push gsiddharth276/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
