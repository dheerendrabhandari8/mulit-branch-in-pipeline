pipeline {
    agent any
  environment {
      Staging_IP = '3.15.166.242'
      Production_IP = '3.14.68.46'
      SSH_cred_staging = 'multi-branch'
      SSH_cred_production = 'ssh-agent' 
    
  }
    stages {
        stage('checkout from staging branch') {
            
            
            
            steps {
                
            git branch: 'staging', credentialsId: 'git_hub', url: 'https://github.com/dheerendrabhandari8/mulit-branch-in-pipeline.git'
            }
        }
   
     stage('deploy in staging') {
        
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['${SSH_cred_staging}']) {

                sh 'ssh -o StrictHostKeyChecking=no root@${Staging_IP}' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@${Staging_IP}:/var/www/html' 
              }
            }
     }
  
        stage('checkout from production branch') {
            
            
            
            steps {
                
            git branch: 'production', credentialsId: 'git_hub', url: 'https://github.com/dheerendrabhandari8/mulit-branch-in-pipeline.git'
            }
        }
 stage('deploy in production') {
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['${SSH_cred_production}']) {

                sh 'ssh -o StrictHostKeyChecking=no root@${Production_IP}' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@${Production_IP}:/var/www/html' 
              }
            }
 
}
    
     }
        
    }
    
    
    //   post {
    //     success {
    //         // Trigger the second job (Pipeline 2) when the first job is successful
    //         build job: 'second_job', propagate: false
    //     }
    // }
    
