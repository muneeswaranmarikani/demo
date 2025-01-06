pipeline {
  environment {
    registry = "munees2027"
    registryCredential = 'Munees22**'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/muneeswaranmarikani/demo.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push Image') {
      steps{
        script {
          /* Finally, we'll push the image with two tags:
                   * First, the incremental build number from Jenkins
                   * Second, the 'latest' tag.
                   * Pushing multiple tags is cheap, as all the layers are reused. */
          docker.withRegistry('https://hub.docker.com/repository/docker/munees2027/cicd-demo/general', 'Munees22**') {
              dockerImage.push("${env.BUILD_NUMBER}")
              dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploy to K8S'){
        steps{
            sh 'kubectl apply -f deployment.yml'
       }
    }
  }
}
