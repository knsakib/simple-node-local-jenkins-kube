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
    stage('Push our image') { 
      steps { 
        script { 
          docker.withRegistry( '', registryCredential ) { 
            dockerImage.push() 
          }
        } 
      }
    }
    stage('Deployment') {
      steps {
        script {
          container('helm') {
            // Init authentication and config for your kubernetes cluster
            sh("helm upgrade --install --wait local-kube ./helm-local-jenkins-kube")
          }
        }
      }
    }
  }  
}
