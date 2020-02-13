#!/usr/bin/groovy

def call() {
node {
   def mvnHome,VERSION
   //stages will be displayed as blocks in the jenkins UI
   stage('Preparation') {
     //will clean the workspace
      cleanWs()

     //get the code checkout from scm
       checkout scm
   }


    stage ('Test') {

      //will pull the dependencies
       sh "mvn clean -DskipTests=true"


    }
   if (env.BRANCH_NAME.startsWith('PR-')){
        stage ('Install') {
          //will run the build with tests for PR build
           sh "mvn clean install"
           cleanWs()
        }
      }

   //Running build with skipping tests for post merge build
   else {
    stage ('Install') {
        //will run the build without tests as they are tested in PR build stage
        sh "mvn clean install -DskipTests=true"
       }
     }
   }
}
