pipeline {

  environment {
    registry = "omidbabaeidocker/docker-test"
    registryCredential = 'dockerhub'
  }

  agent any
  
  stages {
    
    stage('Cloning Git') {
      steps {
        git 'https://github.com/gustavoapolinario/microservices-node-example-todo-frontend.git'
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
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    stage(‘Docker Purge’) {
      steps {
        sh ‘docker image prune -fa’
        deleteDir()
      }
    }
  }
}
