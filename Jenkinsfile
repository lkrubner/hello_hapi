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


        stage('Which branch') {

        try {
            timeout(time: 180, unit: 'SECONDS') { // change to a convenient timeout for you

                userInput = input(
                    id: 'userInput',
                    message: "Which branch do you wish to build?", 
                    parameters: [
                        [$class: 'TextParameterDefinition', defaultValue: "build-${env.BUILD_NUMBER}", description: 'Which branch do you want to test?', name: 'Type the name of the branch:']
                        ])

                listOfDockerTags = userInput.tokenize()
                                
            }
            
        } catch(e) { // timeout reached or input false

            println "An exception occurred during the 'Add tags' stage:"
            println e.getMessage()
            throw e

        }

        println "End of the 'Add tags' stage"
        
    }
    


        stage('Which version of PHP') {

        try {
            timeout(time: 180, unit: 'SECONDS') { // change to a convenient timeout for you

                userInput = input(
                    id: 'userInput',
                    message: "Which version of PHP, 5 or 7?", 
                    parameters: [
                        [$class: 'TextParameterDefinition', defaultValue: "build-${env.BUILD_NUMBER}", description: 'Ask the developer what version this runs on', name: 'PHP 5 or 7?']
                        ])

                listOfDockerTags = userInput.tokenize()
                                
            }
            
        } catch(e) { // timeout reached or input false

            println "An exception occurred during the 'Add tags' stage:"
            println e.getMessage()
            throw e

        }

        println "End of the 'Add tags' stage"
        
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
