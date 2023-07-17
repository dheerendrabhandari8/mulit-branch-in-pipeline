pipeline {
    agent any
    stages {
        stage('Deploy On Staging Environment') {
            environment {
                BRANCH_NAME = 'staging'
            }
            steps {
                script {
                    sshagent(['new-test']) {
                        // sh "ssh -o StrictHostKeyChecking=no root@3.108.250.193 'cd /var/www/html && git reset --hard origin/${BRANCH_NAME} && git pull'"
                        // sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.108.250.193:/var/www/html/'
                       sh 'ssh -o StrictHostKeyChecking=no root@3.110.33.178' 
              sh 'scp -r /var/lib/jenkins/workspace/multiple-branch-insingle-pipeline/* root@3.110.33.178:/var/www/html/'
                    }
                }
            }
        }
    }
}
