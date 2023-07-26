pipeline {
  agent {
    docker { 
      host 'tcp://docker:2375' // Use single quotes for the host URL
      image 'node:18'
      args '-v /var/jenkins_home:/var/jenkins_home' // Mount the workspace directory
    }
  } 
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
