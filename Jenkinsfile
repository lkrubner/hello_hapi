#!/usr/bin/env groovy

node() {


    
    stage('Checkout') {     

        println "Some diagnostic data for debugging "
            
        println "System.getenv(PATH) -- " + System.getenv("PATH")
        println "uname -a -- " + "uname -a".execute().text
        println "whoami -- " + "whoami".execute().text
        println "pwd -- " + "pwd".execute().text
        
        println "The elments in the 'env' variable: "
        echo sh(script: 'env|sort', returnStdout: true)
            
        scmVars = checkout scm        
        println "The return result of the checkout command: "
        for (element in scmVars) {
            println "${element.key} ${element.value}"
        }
            
        echo sh(script: " git show ${scmVars.GIT_COMMIT}  ", returnStdout: true)
        
        println "End of the checkout stage."
    }


        stage('Build') {

                echo 'Building...'
                sh 'npm install'

        }
        stage('Test') {

                echo 'Testing...'
                sh 'npm test'

        }

}
