pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '''-p 3000:3000
RUN  apt-get install -y libltdl7 '''
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Click "Proceed" to continue'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}