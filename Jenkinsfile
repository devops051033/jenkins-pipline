pipeline {
    environment {
        NEW_VERSION = '1.2.0'
        APP_NAME = 'test-app'
    // SERVER_CREDENTIALS = credentials ('server-cred')
    }
    agent any
    stages {
        stage('test') {
            when{
                expression { env.GIT_BRANCH == 'origin/feature-basic-pipline' }
            }
            steps {
                echo "testing the application.....using branch -> ${env.GIT_BRANCH}"
                echo "building app -> ${APP_NAME} version ${NEW_VERSION}"
            }
        }

        stage('build') {
            steps {
                echo 'building the application.....'
            }
        }

        stage('deploy') {
            steps {
                echo 'deploying the application....'
                withCredentials([usernamePassword(credentialsId: 'server-cred', usernameVariable: 'USER', passwordVariable: 'PWD')]) {
                    sh '''
                echo Deploying with user: $USER
                echo some script $USER $PWD
            '''
                }
            }
        }
    }
}
