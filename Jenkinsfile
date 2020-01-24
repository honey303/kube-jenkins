pipeline {
  agent any
  stages {
    stage('Build Docker images') {
      steps {
        sh "docker build ./vote -t honey99/vote:v2"
      }
    }

    stage('DockerHub Push') {
      steps {
        withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerpwd')]) {
            sh "docker login -u honey99 -p ${dockerpwd}"
            sh "docker push honey99/vote:v2"
        }
      }
    }
  }

}
