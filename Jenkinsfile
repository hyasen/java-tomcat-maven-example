pipeline {
    agent any
    stages {
        stage ('Test PipeLine Project') {
            steps {
                /*For windows machine */
               bat  'mvn clean package'
 
                /*For Mac & Linux machine */
               // sh  'mvn clean package'
            }
 
            post{
                success{
                    echo 'Now Archiving ....'
 
                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
 
        stage ('Deploy To Staging Area'){
            steps{
 
                build job : 'Test-PipeLine-Stage'
 
            }
        }
		
		stage ('Deploy to Production'){
            steps{
                timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }
                
                build job : 'Test-PipeLine-Prod'
            }
 
            post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
                }
 
                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
            }
        }
    }
}
