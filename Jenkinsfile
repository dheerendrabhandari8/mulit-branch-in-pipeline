pipeline {
    agent any
    stages {
        stage('deploy') {
                  environment {
                BRANCH_NAME = 'staging'
            }
            steps {
            
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['multi-branch']) {

                sh 'ssh -o StrictHostKeyChecking=no root@13.145.64.16' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@3.145.64.16:/var/www/html' 
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

