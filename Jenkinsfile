pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                script {
                    def deployToProduction = false
                    if (env.BRANCH_NAME == 'main') {
                        deployToProduction = input(message: 'Do you want to deploy on production ??', ok: 'Deploy to Production')
                    } else {
                        deployToProduction = input(message: 'Do you want to deploy on production ??', ok: 'Deploy to Production (Non-Main Branch)')
                    }

                    if (deployToProduction) {
                        sshagent(['your-ssh-credentials-id']) {
                            sh '''
                                ssh -o StrictHostKeyChecking=no root@3.108.250.193 '
                                scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/
                            '''
                        }
                    } else {
                        echo 'Deployment to production skipped.'
                    }
                }
            }
        }
    }
}
