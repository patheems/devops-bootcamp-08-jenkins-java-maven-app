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
                    echo "BRANCH_NAME is ${env.BRANCH_NAME}"
                    return env.BRANCH_NAME == 'feature/jenkins-jobs'
                }
            }
            steps {
                echo "testing the application"
                echo "mvn -version"
            }
        }

        stage("deploy") {
            steps {
                echo "deploying the application"
                echo "deploying with ${SERVER_CREDENTIALS}"

                withCredentials([
                    usernamePassword(credentialsId: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                ]) {
                    sh 'some script ${USER} ${PWD}'
                }
            }
        }
    }
}
