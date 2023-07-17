pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            environment {
                BRANCH_NAME = 'staging'
            }
            steps {
                script {
                    sshagent(['ssh-agent']) {
                        // sh "ssh -o StrictHostKeyChecking=no root@3.108.250.193 'cd /var/www/html && git reset --hard origin/${BRANCH_NAME} && git pull'"
                        // sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                              sh 'ssh -o StrictHostKeyChecking=no root@18.188.202.173' 
     sh ' scp -r /var/lib/jenkins/workspace/php_ssh/*  root@18.188.202.173:/var/www/html' 
                    }
                }
            }
        }
    }
}
