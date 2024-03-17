pipeline {
  environment {
    registry = "lbrik159/tp5"
    registryCredential = 'dockerHub'
    dockerImage = ''
   
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/mbark159/tp5-DP.git'
      }
    }
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test image') {
      steps {
        script {

          echo "Tests passed"
        }
      }
    }
    stage('Publish Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy image') {
       steps{
       sh "docker run -d $registry:$BUILD_NUMBER"
       }
     }
  }
}