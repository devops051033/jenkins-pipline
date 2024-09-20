pipeline {   
    environment {
        NEW_VERSION = '1.2.0'
        APP_NAME = 'test-app'
       // SERVER_CREDENTIALS = credentials ('server-cred')
    }
    agent any
    stages {
        stage("test") {
            steps {
                echo 'testing the application.....'
                echo "building app -> ${APP_NAME} version ${NEW_VERSION}"
            }
        }
        
        stage("build") {
            steps {
                echo 'building the application.....'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application....'
                withCredentials([usernamePassword(credentials: 'server-cred',usernameVariable: USER, passwordVariable: PWD)]){
                    sh "some script ${USER} ${PWD}"
                }
            }
        }               
    }
} 