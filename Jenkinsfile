pipeline {
  environment {
    registry = "iiittarun1625/kubs"
    registryCredential = 'dockerhub'
    dockeruser= "iiittarun1625"
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        git url: 'https://github.com/csetarun2/kubernetes-docker-cicd/'  
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
      }
        }
      }
      stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    
    stage('kubernetes runs') {
      steps{
        sh 'sed -i "s/BUILDNUMBER/$BUILD_NUMBER/" dep.yml'   
                sh 'sed -i "s/DOCKERUSERNAME/' + dockeruser + '/" dep.yml'
        

        sh 'kubectl apply -f dep.yml || echo "nothing to create"' 
      }
    }
    }
  }
