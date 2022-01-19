pipeline {
    agent any
    environment {
        VERSION = '1.3.0'
        // Below gets credentials stored in Jenkins but we won't use this here
        // We'll get the credentials in a wrapper in the deploy stage
        // CREDENTIALS = credentials('pipelineTestCreds')
    }
    //tools {
    //    maven mvn3.8
    //}
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
                    $env.BRANCH_NAME == 'dev' && VERSION == '1.3.0'
                }
            }
            steps {
                echo "building verions ${VERSION}"
                // sh 'echo mvn --version'
            }
        }

        stage('test') {
            // we will only run this stage if the branch name is not master
            when {
                expression {
                    $env.BRANCH_NAME != 'master'
                }
            }
            steps {
                echo 'Running tests'
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploying code'
                withCredentials([
                    usernamePassword(credentialsId: 'pipelineTestCreds', usernameVariable: 'USER', passwordVariable: 'PASS')
                ]) {
                echo "Deploying with credentials: ${USER}, ${PASS}"
                }
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