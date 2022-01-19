pipeline {
    agent any

    stages {
        
        stage('pull source') {
            steps {
                echo 'pulling source from repository'
            }
        }

        stage('build') {
            // we are only going to run this stage if the branch name is dev
            // and it has the tag 'test-release'
            when {
                expression {
                    BRANCH_NAME == 'dev' && TAG_NAME == 'test-release'
                }
            }
            steps {
                echo 'building...'
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
            }
        }
    }
    post {
        always {
            echo 'I always execute'
        }
        success {
            echo 'Build successful'
        }
        failure {
            echo 'Build Failed'
        }
    }
}