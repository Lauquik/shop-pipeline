pipeline {
  agent any
  stages {  
    stage('test') {
      steps {
        sh 'npm install'
        sh 'npm test'
      }
    }
    stage('build') {
      steps {
        sh 'npm install'
        sh 'npm run build' // Use 'npm run build' instead of 'npm build'
      }
    }
  }
}
