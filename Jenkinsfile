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
                expression { changeset "*/**" && env.GIT_BRANCH == 'origin/feature-basic-pipline'}
            }
            steps {
                echo "testing the application using branch -> ${env.GIT_BRANCH}"
                echo "building app -> ${APP_NAME} version ${NEW_VERSION}"
            }
        }

        stage('test-2') {
            when {
                expression { currentBuild.changeSets.size() > 0 }
            }
            steps {
                echo 'Testing the application.....'
                echo "Building app -> ${APP_NAME} version ${NEW_VERSION}"
            }
        }

        stage('check-changes') {
            steps {
                script {
                    def changeLog = ""
                    for (changeSet in currentBuild.changeSets) {
                        for (entry in changeSet.items) {
                            changeLog += "Commit: ${entry.commitId}\n"
                            changeLog += "Author: ${entry.author}\n"
                            changeLog += "Message: ${entry.msg}\n"
                            changeLog += "Affected files:\n"
                            for (file in entry.affectedFiles) {
                                changeLog += "    ${file.path}\n"
                            }
                            changeLog += "\n"
                        }
                    }

                    if (changeLog) {
                        echo "Changes detected:\n${changeLog}"
                    } else {
                        echo "No changes detected in this build."
                    }
                }
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
