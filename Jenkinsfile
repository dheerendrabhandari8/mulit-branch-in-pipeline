pipeline {
    agent any
  environment {
      Staging_IP = '3.145.64.16'
      Production_IP = '3.14.68.46'
      SSH_cred_staging = 'multi-branch'
      SSH_cred_production = 'ssh-agent' 
      Github_url = 'https://github.com/dheerendrabhandari8/mulit-branch-in-pipeline.git'
  }
    stages {
        stage('Hello') {
            
            
            
            steps {
                
            git branch: 'staging', credentialsId: 'git_hub', url: '${Github_url}'
            }
        }
   
     stage('deploy') {
        
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['${SSH_cred_staging}']) {

                sh 'ssh -o StrictHostKeyChecking=no root@${Staging_IP}' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@${Staging_IP}:/var/www/html' 
              }
            }
     }
  
        stage('Hello2') {
            
            
            
            steps {
                
            git branch: 'production', credentialsId: 'git_hub', url: '${Github_url}'  
            }
        }
 stage('deb') {
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
    
