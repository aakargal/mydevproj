pipeline {
  agent any 
  environment {
   version = "${env.BUILD_ID}"

  }

  stages {
    stage("docker build and docker push") {
       steps {
         script {
           withCredentials([string(credentialsId: 'nexus-pass', variable: 'nexus-password')]) {
             sh '''
                docker build -t 3.108.238.215:8083/springapp:${version} .      
                docker login -u admin -p ${nexus-password} 3.108.238.215:8083
                docker push 3.108.238.215:8083/springapp:${version}
                docker rmi 3.108.238.215:8083/springapp:${version}
              '''
           }

        }

      }

   }
      
 }


}
