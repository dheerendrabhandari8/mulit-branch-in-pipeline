pipeline {
    agent any

    stages {
        stage('Hello') {
            
            
            
            steps {
                
            git branch: 'main', credentialsId: 'git_hub', url: 'https://github.com/dheerendrabhandari8/jenkins-cicd-php-demo.git'  
            }
        }
   
     stage('deploy') {
            steps {
                 input 'Do yo want to deploy on staging environment ?'
              sshagent(['muli-branch']) {

                sh 'ssh -o StrictHostKeyChecking=no root@3.145.64.16' 
     sh ' scp -r /var/lib/jenkins/workspace/php_ssh/*  root@3.145.64.16:/var/www/html' 
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
    }
