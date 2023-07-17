pipeline {
    agent any
  environment {
                Staging_IP = '3.145.64.16'
      Production_IP = '3.14.68.46'
            }
    stages {
        stage('Hello') {
            
            
            
            steps {
                
            git branch: 'staging', credentialsId: 'git_hub', url: 'https://github.com/dheerendrabhandari8/mulit-branch-in-pipeline.git'
            }
        }
   
     stage('deploy') {
          environment {
                BRANCH_NAME = 'staging'
            }
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['muli-branch']) {

                sh 'ssh -o StrictHostKeyChecking=no root@Staging_IP' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@Staging_IP:/var/www/html' 
              }
            }
     }
  
        stage('Hello2') {
            
            
            
            steps {
                
            git branch: 'production', credentialsId: 'git_hub', url: 'https://github.com/dheerendrabhandari8/mulit-branch-in-pipeline.git'  
            }
        }
 stage('deb') {
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['ssh-agent']) {

                sh 'ssh -o StrictHostKeyChecking=no root@Production_IP' 
     sh ' scp -r /var/lib/jenkins/workspace/new-mb/*  root@Production_IP:/var/www/html' 
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
    
