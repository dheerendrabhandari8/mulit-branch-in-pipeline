pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                input 'Do you want to deploy on staging??'
                env.BRANCH_NAME = 'staging'
                sshagent(['new-test']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@3.108.250.193 "cd /var/www/html && git reset --hard origin/${env.BRANCH_NAME} && git pull"'
                    sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                }
            }
        }

        stage('Deploy On Production Environment') {
            steps {
                input 'Do you want to deploy on production??'
                env.BRANCH_NAME = 'production'
                sshagent(['new-test']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@3.108.250.193 "cd /var/www/html && git reset --hard origin/${env.BRANCH_NAME} && git pull"'
                    sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                }
            }
        }
    }
}
