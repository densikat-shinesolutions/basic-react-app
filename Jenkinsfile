pipeline {
  agent { label 'slave' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  tools {
    nodejs 'node'
  }
  stages {
    stage('npm install'){
      steps{
         sh "npm install"
      }
    }
    stage('npm build'){
      steps{
        sh "npm run build"
      }
    }
    stage('docker build'){
      steps{
        script {
          docker.build('basic-react-app')
        }
      }
    }
    stage('docker push'){
      steps{
        script {
          docker.withRegistry('portabledave/basic-react-app', '822d4685-d1fe-4628-a373-84744cdb8327') {
            docker.image('basic-react-app').push('latest')
          }
        }
      }
    }
  }
  post {
    always {
      sh 'echo "This will always run"'
    }
  }
}
