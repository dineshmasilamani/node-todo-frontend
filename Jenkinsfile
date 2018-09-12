pipeline {
  environment {
    registry = 'dineshmasilamani5/transporter_test'
    registryCredential = 'Smileplease@1'
    dockerImage = ‘’
  }
  agent any
  stages {
    stage(‘Cloning Git’) {
      steps {
        git 'https://github.com/dineshmasilamani/node-todo-frontend.git'
      }
    }
    stage(‘Building image’) {
      steps{
        script {
          dockerImage = docker.build registry + “:$BUILD_NUMBER”
        }
      }
    }
    stage(‘Deploy Image’) {
      steps{
        script {
          docker.withRegistry( ‘’, registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
