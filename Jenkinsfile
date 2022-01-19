pipeline {
    agent any
    environment {
        VERSION = '1.3.0'
        CREDENTIALS = credentials('pipelineTestCreds')
    }
    stages {
        
        stage('pull source') {
            steps {
                echo 'pulling source from repository'
            }
        }

        stage('build') {
            // we are only going to run this stage if the branch name is dev
            // and the version is 1.3.0
            when {
                expression {
                    BRANCH_NAME == 'dev' && VERSION == '1.3.0'
                }
            }
            steps {
                echo "building verions ${VERSION}"
            }
        }

        stage('test') {
            // we will only run this stage if the branch name is not master
            when {
                expression {
                    BRANCH_NAME != 'master'
                }
            }
            steps {
                echo 'Running tests'
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploying code'
                echo "Deploying with credentials: ${CREDENTIALS}"
            }
        }
    }
    post {
        always {
            echo 'I always execute'
        }
        success {
            echo 'I only execute when build is successful'
        }
        failure {
            echo 'I only execute when build failed'
        }
    }
}