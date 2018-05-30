pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''node --version
npm --version
npm install'''
      }
    }
    stage('Unit Test') {
      parallel {
        stage('Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }
        stage('Chrome Tests') {
          steps {
            sh 'echo "Chrome tests mock"'
          }
        }
        stage('Firefox Tests') {
          steps {
            sh 'echo "Firefox tests mock"'
          }
        }
        stage('Component Tests') {
          steps {
            sh 'echo "Component Tests mock"'
          }
        }
        stage('Integration Tests') {
          steps {
            sh 'echo "Integration Tests mock"'
          }
        }
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}