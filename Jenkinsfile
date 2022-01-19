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
}