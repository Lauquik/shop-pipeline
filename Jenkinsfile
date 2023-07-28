pipeline {
  agent any
    options {
        tools {
            sonarscanner 'sonarscanner'
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
        sh 'npm run build'
      }
    }

    stage('sonar analysis'){
      steps{
        withSonarQubeEnv('sonarserver') {
          sh "sonar-scanner -Dsonar.token=squ_fda766faa93bd7b3107e92d1d3272f08846ceb5c"
        }
      }
    }
  }
}
