
// make a variable for our external script
def gv

pipeline {
    agent any
    environment {
        VERSION = '1.3.0'
        // Below gets credentials stored in Jenkins but we won't use this here
        // We'll get the credentials in a wrapper in the deploy stage
        // CREDENTIALS = credentials('pipelineTestCreds')
    }
    tools {
        maven 'mvn3.8'
        jdk 'OpenJDK11'
        gradle 'grdl7.3'
    }
    parameters {
        string(name: 'RANDOMSTRING', defaultValue: 'A Random String', description: 'This is a random string')
        choice(name: 'VERSIONTODEPLOY', choices: ['1.1.0', '1.1.1', '1.1.2'], description: '')
        booleanParam(name: 'EXECUTETESTS', defaultValue: true, description: 'Execute the tests')
    }
    stages {
        // Loads external scripts
        stage("init") {
                steps {
                    script {
                        gv = load "script.groovy"
                    }
                }
        }
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
                script {
                    gv.build()
                }
                echo "building verions ${VERSION}"
                withMaven() {
                    sh 'mvn -v'
                }    
                sh 'echo "JDK Version: $(javac -version)"' 
                with nodejs('Node17.4') {
                    sh 'echo "NPM Version: $(npm --version; yarn install)"'    
                }
                sh 'echo "Gradle Version: $(gradlew -v)"'
            }
        }

        stage('test') {
            // we will only run this stage if the branch name is not master
            when {
                expression {
                    BRANCH_NAME != 'master' && params.EXECUTETESTS
                }
            }
            steps {
                script {
                    gv.test()
                }
            }
        }

        stage('deploy') {
            steps {
                echo 'Deploying code'
                withCredentials([
                    usernamePassword(credentialsId: 'pipelineTestCreds', usernameVariable: 'USER', passwordVariable: 'PASS')
                ]) {
                echo "Deploying version ${params.VERSIONTODEPLOY} with credentials: ${USER}, ${PASS}"
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