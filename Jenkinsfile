pipeline {
    agent any
    environment {
        BRANCH_NAME = 'staging'
    }
    stages {
        stage('Deploy On Staging Environment') {
            steps {
                sshagent(['new-test']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@3.108.250.193 "cd /var/www/html && git reset --hard origin/${BRANCH_NAME} && git pull"'
                    sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                }
            }
        }

        stage('Deploy On Production Environment') {
            steps {
                BRANCH_NAME = 'production'
                sshagent(['new-test']) {
                    sh 'ssh -o StrictHostKeyChecking=no root@3.108.250.193 "cd /var/www/html && git reset --hard origin/${BRANCH_NAME} && git pull"'
                    sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                }
            }
        }
    }
}
