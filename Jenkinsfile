pipeline {
  agent none
  stages {
    stage('test') {
      agent{
        label 'agent0'
      }
    //   steps {
    //     checkout scm
    //     sh 'npm install'
    //     sh 'npm test'
    //   }
    // }
    // stage('build') {
    //   steps {
    //     sh 'npm install'
    //     sh 'npm run build'
    //   }
    // }
    // stage('sonar analysis'){
    //   environment {
    //       scannerHome = tool "sonarscanner"
    //   }
    //   steps{
    //     withSonarQubeEnv('sonarserver') {
    //       sh "${scannerHome}/sonar-scanner -Dsonar.token=squ_db7b447f961deb315feb53d52b41b8edf52ef8ec"
    //     }
    //   }
    // }
    stage('docker build') {
      agent{
        label 'agent1'
      }
      steps{
        checkout scm
            script {
                def dockerImageTag = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
                docker.build("myshoppapp:${dockerImageTag}")
            }
      }
    }
  }
}
