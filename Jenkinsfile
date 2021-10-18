pipeline {
  agent any 
  environment {
   version = "${env.BUILD_ID}"

  }

  stages {
    stage("docker build and docker push") {
       steps {
         script {

           withCredentials([string(credentialsId: 'docker-password', variable: 'docker-pass')]) {
          sh '''
            docker build -t amol273/myrespository:${version} .
            docker login -u amol273 -p $docker-pass 
            docker push amol273/myrespository:${version}
            docker rmi amol273/myrespository:${version}

          '''
          }
         }
      
       }

   }

  }

}
