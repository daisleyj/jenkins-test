pipeline {
    agent any

    stages {
        
        stage('pull source') {
            steps {
                echo 'pulling source from repository'
            }
        }

        stage('build') {
            steps {
                echo 'building...'
            }
        }

        stage('test') {
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