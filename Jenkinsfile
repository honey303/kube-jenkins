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
          sshagent(['a4a7643e-7e73-4726-9062-f5eb714cb828']) {
            script {
              sh "sh ubuntu@ec2-18-207-206-71.compute-1.amazonaws.com sudo kubectl set image deployment/db postgres=postgres:9.4 -n vote"
            }
          }

      }
    }
  }

}
