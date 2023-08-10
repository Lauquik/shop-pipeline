pipeline {
  agent none

  environment {

    Container_Registry = '453947716429.dkr.ecr.us-east-1.amazonaws.com/myshopapp'
    Regisry_URL = 'http://453947716429.dkr.ecr.us-east-1.amazonaws.com/myshopapp'

  }

  stages {
    stage('test') {
      agent{
        label 'agent0'
      }
      steps {
        sh 'npm install'
        sh 'npm test'
      }
    }

    stage('build') {
      agent{
        label 'agent1'
      }
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }

    stage('docker build') {
      agent{
        label 'agent1'
      }
      steps{
        dockerImage = docker.build( Container_Registry + ":$BUILD_NUMBER")
      }
    }


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
  }
}
