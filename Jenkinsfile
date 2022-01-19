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
                sh 'npm install'
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