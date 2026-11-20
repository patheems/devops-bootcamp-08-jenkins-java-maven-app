#!/user/bin/env groovy

library identifier: "jenkins-shared-library@main", retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/patheems/devops-bootcamp-08-jenkins-jenkins-shared-library.git',
    credentialsId: 'github-credentials'])
def gv

pipeline {
    agent any
    tools {
        maven 'maven-3.10'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage("build and push image") {
            steps {
                script {
                    buildImage 'justphit/demo-app:jma-4.0'
                    dockerLogin()
                    dockerPush 'justphit/demo-app:jma-4.0'
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
