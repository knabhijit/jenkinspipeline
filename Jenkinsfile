pipeline {
    agent any
    
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
 
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        build job: 'Deploy-to-staging'
                    }
                }
 
                stage ("Deploy to Production"){
                    steps {
                        build job: 'Deploy-to-Prod'
                    }
                }
            }
        }
    }
}
