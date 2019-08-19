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
          docker.withRegistry('https://541837530073.dkr.ecr.ap-southeast-2.amazonaws.com/basic-react-app', 'ecr:ap-southeast-2:ecrpush') {
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
