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
               
               
               sh " kubectl apply -f kaniko-git.yaml -n jenkins"
               sh "kubectl wait --for condition=containersready pod kaniko -n jenkins"
               sh "kubectl logs -f kaniko -n jenkins"
        }
      }
    }  
   
  }
}
