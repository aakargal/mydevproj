pipeline {
  agent any 
  environment {
   version = "${env.BUILD_ID}"

  }

  stages {
    stage("docker build and docker push") {
       steps {
         script {
            withDockerRegistry(credentialsId: 'docker-credential', url: 'https://registry-1.docker.io/v2/') {
             def customImage = docker.build("amol273/myrespository:${env.BUILD_ID}")

             customImage.push()
  
            }

          }

         }
      
       }

   }

}
