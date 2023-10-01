pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t shyfur/jenkins-docker .'
      }
    }
   /* stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }*/
    stage('Push') {
      steps {
        sh "sudo docker login -u 'axf5p8j94qn5/md.shyfur.rahman@oracle.com' -p 'mjw3wpu*gpq5QBV8cdv' sin.ocir.io" 
        sh "sudo docker tag customimage:1 sin.ocir.io/axf5p8j94qn5/customimage:1" 
        sh 'sudo docker push sin.ocir.io/axf5p8j94qn5/customimage:1'
        /* sh 'docker push shyfur/jenkins-docker' */
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}