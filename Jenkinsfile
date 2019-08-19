pipeline {
  agent any
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
        sh "docker build ."
      }
    }
  }
  post {
    always {
      sh 'echo "This will always run"'
    }
  }
}
