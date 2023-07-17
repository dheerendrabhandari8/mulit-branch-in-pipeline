pipeline {
    agent any
    stages {
       
        stage('Deploy On Staging Environment') {

                steps {
              input 'Do you want to deploy on production ??'
        if (env.BRANCH_NAME == 'main') {
sshagent(['new-test']) {
              sh 'ssh -o StrictHostKeyChecking=no root@3.108.250.193' 
              sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
              }
            }
        } else {
             input 'Do you want to deploy on production ??'

               sh 'ssh -o StrictHostKeyChecking=no root@3.110.33.178 '
           // hello
        }
            }
        }
        }
        
    
