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
        sh 'npm run build'
      }
    }

    stage('sonar analysis'){
      steps{
        environment {
            scannerHome = tool "sonarscanner"
        }
        withSonarQubeEnv('sonarserver') {
          sh "${scannerHome}/sonar-scanner -Dsonar.token=squ_fda766faa93bd7b3107e92d1d3272f08846ceb5c Dsonar.projectName=shoppin"
        }
      }
    }
  }
}
