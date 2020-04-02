pipeline {
    agent any
        environment {
            DEPLOY_PROFILE = "${env.BRANCH_NAME == "develop" ? "staging" : "production"}"
        }

    stages {
        stage('Environment') {
            steps {
                script {
                    // Determine
                    sh "echo Branch is $BRANCH_NAME"
                    script {
                        if (${env.BRANCH_NAME == "production"}) {
                            env.DEPLOY_PROFILE = 'stage-prod'
                        } else {
                            if (${env.BRANCH_NAME == "candidate"}) {
                                env.DEPLOY_PROFILE = 'stage-test'
                            } else {
                                env.DEPLOY_PROFILE = 'stage-dev'
                            }
                        }
                    }
                    sh "echo Deployprofile is $DEPLOY_PROFILE"
                }
            }
        }

        stage('build') {
            steps {
                sh "echo $DEPLOY_PROFILE"
                sh 'mvn --version'
            }
        }
    }
}