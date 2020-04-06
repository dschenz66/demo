pipeline {
    agent any
        environment {
            DEPLOY_PROFILE = "${env.BRANCH_NAME == "develop" ? "staging" : "production"}"
            MY_VAR="${DEPLOY_PROFILE}/selfservice-core"
        }

    stages {
        stage('Environment') {
            steps {
                script {
                    // Determine npm profile
                    sh "echo Branch is $BRANCH_NAME"
                    script {
                        switch (env.BRANCH_NAME) {
                            case 'master':
                                env.NPM_ENV = 'stage-prod'
                                break
                            case 'candidate':
                                env.NPM_ENV = 'stage-test'
                                break
                            case 'development':
                                env.NPM_ENV = 'stage-dev'
                                break
                            default:
                                env.NPM_ENV = 'unknown'
                        }
                    }
                    sh "echo npm-profile is $NPM_ENV"
                }
            }
        }

        stage('build') {
            steps {
                sh "echo $NPM_ENV"
                sh 'mvn --version'
            }
        }
    }
}