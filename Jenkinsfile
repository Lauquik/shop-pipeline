pipeline{
  agent{
    docker {image: 'node:18'}
  } 
  stages{

    stage('test'){
      steps{
          sh 'npm install'
          sh 'npm test'
      }
    }
    stage('build'){
      steps{
        sh 'npm install'
        sh 'npm build'
      }
    }

  }

}