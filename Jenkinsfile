pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
          git branch: 'main', credentialsId: 'GITHUB_TOKEN', url: 'https://github.com/sagarshrestha24/dashboard.git'

          sh 'git checkout -b main || true'
          
      }
    }
    stage('Build and push image') {
      steps{
        script {
               

               sh "kubectl delete pod kaniko"

               sh " kubectl apply -f kaniko-git.yaml"
               sh "kubectl wait --for condition=containersready pod kaniko"
               sh "kubectl logs -f kaniko"
        }
      }
    }  
   
  }
}
