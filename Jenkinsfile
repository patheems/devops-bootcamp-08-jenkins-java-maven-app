pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }
    tools {
        maven "maven-3.10"
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description:'version to deploy on prod')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
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
                     params.executeTests
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
                echo "deploying version ${params.VERSION}"
            }
        }
    }
}
