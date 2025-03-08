@Library('jenkins_shared_library@develop') _

pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'GIT_Admin'  // Replace with your Jenkins credentials ID
    }

    stages {
        stage('Cleanup') {
            steps {
                cleanWs()  // This will delete everything in the workspace before running the pipeline
            }
        }
        
        stage('Checkout Code') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.GIT_CREDENTIALS_ID, 
                                                     usernameVariable: 'GIT_USERNAME', 
                                                     passwordVariable: 'GIT_PASSWORD')]) {
                        sh 'git clone -b develop https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/SpandanaManthena/task-management-system.git'
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
