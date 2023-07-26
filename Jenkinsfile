pipeline{
  agent{
    docker { 
      label 'doggy'
    }
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