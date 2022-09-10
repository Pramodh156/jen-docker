pipeline {
  environment {
    imagename = "pramodh156/maven1"
    registryCredential = 'pramodh156-dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/Pramodh156/jen-docker.git', branch: ''])

      }
    }
    stage('Building custom image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy custom Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Docker Run Tomcat') {
     steps{
         script {
            dockerImage.run("-p 8093:8080 --rm --name pramodh1")
         }
     }
    }
    
    }
  }
