pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                script {
                     (env.BRANCH_NAME == 'staging') {
                        deployToStaging = input(message: 'Do you want to deploy on staging environment?', ok: 'Deploy staging')
                    
                            sshagent(['your-ssh-credentials-id']) {
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
