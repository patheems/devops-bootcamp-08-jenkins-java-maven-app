pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }
    tools {
        maven "maven-3.10"
    }

    stages {
        stage("build") {
            steps {
                echo "building the application"
                echo "building version ${NEW_VERSION}"
            }
        }

        stage("test") {
            when {
                expression {
                     echo "GIT_BRANCH is ${env.GIT_BRANCH}"
                     return env.GIT_BRANCH == 'origin/feature/jenkins-jobs'
                }
            }
            steps {
                echo "testing the application"
                sh 'mvn -version'
            }
        }

        stage("deploy") {
            steps {
                echo "deploying the application"
                echo 'deploying with $SERVER_CREDENTIALS_USR'

                withCredentials([
                    usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')
                ]) {
                    sh 'echo "deploying with $USER and $PASS"'
                }
            }
        }
    }
}
