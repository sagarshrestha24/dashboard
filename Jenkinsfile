pipeline {
 agent any
        stages {
         
<<<<<<< HEAD
        stage('Push Image') {
                steps{
                    script {
               sh "kubectl delete pod kaniko"
               sh " kubectl apply -f kaniko-git.yaml"
               sh "kubectl wait --for condition=containersready pod kaniko"
               sh "kubectl logs -f kaniko"
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
=======
//         stage('Push Image') {
//                 steps{
//                     script {
//                sh "kubectl delete pod kaniko"
//                sh " kubectl apply -f kaniko-git.yaml"
//                sh "kubectl wait --for condition=containersready pod kaniko"
//                sh "kubectl logs -f kaniko"
//                         }
//                     }
                
//                 post{
//                     success{
//                         echo "Build and Push Successfully"
//                     }
//                     failure{
//                         echo "Build and Push Failed"
//                     }
//                 }
//         }
>>>>>>> 5340741e722f5e51e199841f068e600cd27ec93a
       stage("Deploy to Production"){
            when {
                branch 'main'
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
         stage('Build adsbrain-feed-etl/') {
            when {
                changeset "adsbrain-feed-etl/**"
            }
            steps {
                echo 'changed in adsbrain-feed-etl/'
            }
        }
        stage('Build ch1-2-migration ') {
            when {
                changeset "ch1-2-migration/**"
            }
            steps {
                echo 'changed in Build ch1-2-migration'
            }
        }
    }
}
