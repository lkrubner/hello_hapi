#!/usr/bin/env groovy

node() {


        stage('Build') {
            step {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            step {
                echo 'Testing...'
                sh 'npm test'
            }
        }

}
