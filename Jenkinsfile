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
      environment {
          scannerHome = tool "sonarscanner"
      }
      steps{
        withSonarQubeEnv('sonarserver') {
          sh "${scannerHome}/sonar-scanner -Dsonar.token=squ_db7b447f961deb315feb53d52b41b8edf52ef8ec"
        }
      }
    }
  }
}
