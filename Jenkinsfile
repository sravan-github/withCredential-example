pipeline {
    agent any 

    stages {
        stage('Cloning Git') {
            steps {
                sh '''
                   #!/bin/bash  
                   git clone https://github.com/sravan-github/toolkit.git
                   cd toolkit
                   ls -l
                   cp /var/lib/jenkins/workspace/test-pipeline/toolkit/Dockerfile /var/lib/jenkins/workspace/test-pipeline/Dockerfile
                   '''
            }
        }

       stage('Docker build'){
         steps {
          sh 'docker version'
          sh 'docker build -t toolkit-test .'
          sh 'docker image list'
          sh 'docker tag toolkit-test sravangcpdocker/toolkit-test:4.0'
         }
       }
       stage('login & push'){
         steps {
           script {
           withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB_PASSWORD', passwordVariable: 'password', usernameVariable: 'username')]) {
           sh 'docker login -u $username -p $password'
           sh 'docker push  sravangcpdocker/toolkit-test:4.0'
           }         
        }
      }
    }
       
  }

   post {
        always {
            cleanWs deleteDirs: true
        }
     }

}
