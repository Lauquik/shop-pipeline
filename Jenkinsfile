pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'npm install' // Install dependencies
        sh 'npm test'    // Run tests
      }
    }

    stage('Build') {
      steps {
        sh 'npm install'      // Install dependencies (optional, in case you haven't installed them in the test stage)
        sh 'npm run build'    // Build your Node.js application
      }
    }
  }
}