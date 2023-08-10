def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline {
  agent none

  environment {
    Container_Registry = '453947716429.dkr.ecr.us-east-1.amazonaws.com/myshopapp'
    Regisry_URL = 'http://453947716429.dkr.ecr.us-east-1.amazonaws.com/myshopapp'
    cluster = 'cicdcluster'
    service = 'myshopappservice'
  }
  
  stages {

    stage('checkOut'){
      agent {
        label 'agent0'
      }
      steps { 
        checkout scm
      }
    }
    
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

    stage('sonar analysis'){
      agent {
        label 'agent0'
      }
      environment {
          scannerHome = tool "sonarscanner"
      }
      steps{
        withSonarQubeEnv('sonarserver') {
          sh "${scannerHome}/sonar-scanner"
        }
      }
    }

    stage('build docker image') {
      agent{
        label 'agent1'
      }
      steps{
        script{
          dockerImage = docker.build( Container_Registry + ":$BUILD_NUMBER")
        }
      }
    }

    stage('push docker image'){
      agent{
        label 'agent1'
      }
      steps{
        script {
          docker.withRegistry( Regisry_URL, 'ecr:us-east-1:awscreds') {
            dockerImage.push('latest')
          }
        }
      }
    }

    stage('deploy to ECS'){
      agent{
        label 'agent1'
      }
      steps {
          withAWS(credentials: 'awscreds', region: 'us-east-1') {
              sh "aws ecs update-service --cluster ${cluster} --service ${service} --force-new-deployment"
          }
      }
    }
  }

  post {
      always {
          echo "PIPELINE EXECUTED SUCCESSFULLY"
          echo 'Sending Slack Notifications.'
          slackSend channel: '#devops',
              color: COLOR_MAP[currentBuild.currentResult],
              message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
      }
  }

}
