pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                    input 'Do you want to deploy on production ??'
                script {
                  
                     (env.BRANCH_NAME == 'staging') {
                  
                    
                            sshagent(['new-test']) {
                                sh '''
                                    ssh -o StrictHostKeyChecking=no root@3.108.250.193 '
                                    scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/
                                '''
                            }        
                        }
                    }
                    
        }

        }
    }
    }
