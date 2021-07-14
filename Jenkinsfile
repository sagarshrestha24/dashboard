pipeline {
 agent any
        stages {
         
        stage('Push Image') {
                steps{
                    script {
               sh "kubectl delete pod kaniko"
               sh " kubectl apply -f kaniko-git.yaml"
               sh "kubectl wait --for condition=containersready pod kaniko"
               sh "kubectl logs -f kaniko"
                        }
                    }
                }
                post{
                    success{
                        echo "Build and Push Successfully"
                    }
                    failure{
                        echo "Build and Push Failed"
                    }
                }
        }
       stage("Deploy to Production"){
            when {
                branch 'master'
            }
            steps { 
                echo 'we are in master branch'
             }
            post{
                success{
                    echo "Successfully deployed to Production"
                }
                failure{
                    echo "Failed deploying to Production"
                }
            }
        }
stage("Deploy to Develop"){
            when {
                branch 'develop'
            }
            steps {
                echo 'we are in Develop branch'
             }
            post{
                success{
                    echo "Successfully deployed to Develop"
                }
                failure{
                    echo "Failed deploying to Develop"
                }
            }
        }
   stage('Build Release') {
            when {
                tag pattern: '^release-*', comparator: "REGEXP"
            }
     steps {
        echo 'tags added'
     }
        }
    }
}
