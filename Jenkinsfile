pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
          git branch: 'main', credentialsId: 'GITHUB_TOKEN', url: 'https://github.com/sagarshrestha24/dashboard.git'
      }
    }
      
   
  }
}
