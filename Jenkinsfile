pipeline {
  environment {
    registry = 'https://hub.docker.com'
    registryCredential = 'dineshmasilamani5/transporter_test'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/dineshmasilamani/node-todo-frontend.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry('https://hub.docker.com','dineshmasilamani5/transporter_test') {
            dockerImage.push()
          }
        }
      }
    }
  }
}
