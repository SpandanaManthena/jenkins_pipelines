@Library('jenkins_shared_library') _

pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'GIT_Admin'  // Replace with your Jenkins credentials ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.GIT_CREDENTIALS_ID, 
                                                     usernameVariable: 'GIT_USERNAME', 
                                                     passwordVariable: 'GIT_PASSWORD')]) {
                        sh 'git clone https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/SpandanaManthena/jenkins_shared_library.git'
                    }
                }
            }
        }

        stage('Build Backend') {
            steps {
                mavenBuild()
            }
        }

        stage('Build Frontend') {
            steps {
                reactJSBuild()
            }
        }
    }
}
