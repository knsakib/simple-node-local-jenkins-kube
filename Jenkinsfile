pipeline {
  environment {
    registry = "knsakib/simple-node-local-jenkins-kube" 
    registryCredential = '4ac13e38-8252-49a6-92f1-e2bcd019ade0' 
    dockerImage = ''
    CI = 'true'
  }
  agent any
  stages {
    stage('Building our image') { 
      steps { 
        script { 
          dockerImage = docker.build registry
        }
      } 
    }
    stage('Deploy our image') { 
      steps { 
        script { 
          docker.withRegistry( '', registryCredential ) { 
            dockerImage.push() 
          }
        } 
      }
    }
  }  
}
