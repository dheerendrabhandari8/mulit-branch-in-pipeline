pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                script {
                    def deployToStaging = false
                    if (env.BRANCH_NAME == 'staging') {
                        deployToStaging = input(message: 'Do you want to deploy on production ??', ok: 'Deploy staging')
                     (deployToStaging) {
                        sshagent(['your-ssh-credentials-id']) {
                            sh '''
                                ssh -o StrictHostKeyChecking=no root@3.108.250.193 '
                                scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/
                            '''
                        }
                     }
                    } else if(env.BRANCH_NAME == 'production') {
                          sshagent(['your-ssh-credentials-id']) {
                            sh '''
                         deployToProduction = input(message: 'Do you want to deploy on production ??', ok: 'Deploy to Production')
                       sh 'ssh -o StrictHostKeyChecking=no root@3.110.33.178'
                       '''
                    }
                }
            }
        }
    }
}
