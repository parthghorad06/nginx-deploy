pipeline {
  agent any
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Build Image') { steps { sh 'docker build -t nginx-demo:${BUILD_NUMBER} .' } }
    stage('Deploy') {
      steps {
        sh '''
          docker rm -f nginx_demo || true
          docker run -d --name nginx_demo -p 8081:80 --restart unless-stopped nginx-demo:${BUILD_NUMBER}
        '''
      }
    }
  }
}
