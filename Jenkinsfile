pipeline {
    agent any
    environment {
        STAGING_BRANCH = 'staging'
        PRODUCTION_BRANCH = 'production'
        STAGING_SERVER = '3.108.250.193'
        PRODUCTION_SERVER = '3.110.33.178'
    }
    stages {
        stage('Clone and Deploy to Staging') {
            when {
                branch pattern: STAGING_BRANCH
            }
            steps {
                script {
                    def deployToStaging = input(
                        message: 'Do you want to deploy to staging server?',
                        ok: 'Deploy to Staging',
                        parameters: [booleanParam(defaultValue: true, description: 'Proceed with staging deployment?', name: 'deployToStaging')]
                    )
                    if (!deployToStaging) {
                        error('Staging deployment aborted by user.')
                    }
                }
                steps {
                    checkout scm
                    script {
                        deployToStagingServer()
                    }
                }
            }
        }
        stage('Deploy to Production') {
            when {
                branch pattern: PRODUCTION_BRANCH
                expression { currentBuild.previousBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                script {
                    def deployToProduction = input(
                        message: 'Do you want to deploy to production server?',
                        ok: 'Deploy to Production',
                        parameters: [booleanParam(defaultValue: true, description: 'Proceed with production deployment?', name: 'deployToProduction')]
                    )
                    if (deployToProduction) {
                        checkout([$class: 'GitSCM', branches: [[name: "refs/heads/${PRODUCTION_BRANCH}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: "${env.GIT_URL}"]]])
                        script {
                            deployToProductionServer()
                        }
                    } else {
                        error('Production deployment aborted by user.')
                    }
                }
            }
        }
    }
}

def deployToStagingServer() {
    sshagent(['new-test']) {
        sh "ssh -o StrictHostKeyChecking=no root@${STAGING_SERVER} 'cd /var/www/html && git reset --hard origin/${STAGING_BRANCH} && git pull'"
    }
}

def deployToProductionServer() {
    sshagent(['prod-keys']) {
        sh "ssh -o StrictHostKeyChecking=no root@${PRODUCTION_SERVER} 'cd /var/www/html && git reset --hard origin/${PRODUCTION_BRANCH} && git pull'"
    }
}
