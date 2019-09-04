/* NOTE: this Pipeline mainly aims at catching mistakes (wrongly formed Dockerfile, etc.)
 * This Pipeline is *not* used for actual image publishing.
 * This is currently handled through Automated Builds using standard Docker Hub feature
*/
pipeline {
    agent { label 'slave_node' }

    options {
        timeout(time: 2, unit: 'MINUTES')
        buildDiscarder(logRotator(daysToKeepStr: '10'))
        timestamps()
    }

    triggers {
        pollSCM('H/24 * * * *') // once a day in case some hooks are missed
    }

    //stages {
      //  stage('Build Docker Image') {
        //    steps {
          //      deleteDir()
            //    checkout scm
              //  sh 'make build'
            //}
       // }
    //}
    
    
     stages {
         stage ('Build && push'){
             steps {
                 script{
               checkout scm

                 docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {

                 def customImage = docker.build("maniengg/jenkins4evaljnlpslave")

                 customImage.push()
                 customImage.pull()    
                 }
              }
            }
         }
     }
}

// vim: ft=groovy
