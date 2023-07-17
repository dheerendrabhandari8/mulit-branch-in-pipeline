pipeline {
    agent any
    stages {
        stage('deploy') {
                  environment {
                BRANCH_NAME = 'staging'
            }
            steps {
            
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['ssh-agent']) {

                sh 'ssh -o StrictHostKeyChecking=no root@18.188.202.173' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@18.188.202.173:/var/www/html' 
              }
            }
 

    
     }
        
    }
      post {
        success {
            // Trigger the second job (Pipeline 2) when the first job is successful
            build job: 'second_job', propagate: false
        }
    }
    }

