pipeline {
  agent any
  stages {
    stage('Build Docker images') {
      steps {
        sh "sudo docker build ./vote -t honey99/vote:v2"
      }
    }

    stage('DockerHub Push') {
      steps {
        withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerpwd')]) {
            sh "sudo docker login -u honey99 -p ${dockerpwd}"
            sh "sudo docker push honey99/vote:v2"
        }
      }
    }

    stage('Deploy to K8s') {
      steps {
        sh " echo 'testing the webhook' "
      }
    }
  }

}
