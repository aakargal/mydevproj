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
   stage("indentifying miconfing using datree in helm charts") {
      steps {
        scripts {

         withEnv(['DATREE_TOKEN=Bti6Yt54jTaetLyT5zpbyH']) {

           sh 'helm datree test myapp/'

         }
          
        }
     } 

   }
   stage("pushing helm charts to repository") {
      withCredentials([string(credentialsId: 'docker-password', variable: 'docker_password')]) {    
        sh '''
           helmversion
           curl -u admin:$docker_password http://3.22.44.105:8081/helm_hosted --upload-file myapp:${helmversion}.tgz

       '''
      }
   }

      
 }


}
