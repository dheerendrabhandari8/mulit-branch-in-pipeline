pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                script {
                    def deployToStaging = false
                    if (env.BRANCH_NAME == 'staging') {
                        deployToStaging = input(message: 'Do you want to deploy on staging environment?', ok: 'Deploy staging')
                    
                            sshagent(['your-ssh-credentials-id']) {
                                sh '''
                                    ssh -o StrictHostKeyChecking=no root@3.108.250.193 '
                                    scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/
                                '''
                            
                        }
                    } if (env.BRANCH_NAME == 'production') {
                        def deployToProduction = input(message: 'Do you want to deploy on production environment?', ok: 'Deploy to Production')
                        sshagent(['your-ssh-credentials-id']) {
                                sh 'ssh -o StrictHostKeyChecking=no root@3.110.33.178'
                            }
                        
                    } else {
                        echo "No deployment necessary for branch: ${env.BRANCH_NAME}"
                    }
                }
            }
        }
    }
}
