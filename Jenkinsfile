pipeline {   
    environment {
        NEW_VERSION = '1.2.0'
        APP_NAME = 'test-app'
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
            }
        }               
    }
} 