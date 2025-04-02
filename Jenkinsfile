pipeline {
    agent {
        docker {
            image 'node:20-alpine'
        }
    }
    stages {
        stage('Building') {
            steps {
                sh 'npm install -g firebase-tools'
            }
        }
        stage('Testing') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh '''
                        firebase deploy -P testing-aa739 --token "$FIREBASE_TOKEN"
                    '''
                }
            }
        }
        stage('Staging') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh '''
                        firebase deploy -P staging-380a6 --token "$FIREBASE_TOKEN"
                    '''
                }
            }
        }
        stage('Production') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh '''
                        firebase deploy -P sqa113-devops-36277 --token "$FIREBASE_TOKEN"
                    '''
                }
            }
        }
    }
}