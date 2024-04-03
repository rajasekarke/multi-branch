pipeline {
    agent any
    tools {
        maven 'maven' 
    }
    stages {
      stage ('Build') {
        steps {
          script{
            def mvnHome = tool name: 'maven', type: 'maven'
            sh "${mvnHome}/bin/mvn clean package"
              sh 'mv target/onlinebookstore*.war target/newapp.war'
              // sh "mvn clean package"
              // sh "mv target/*.war target/newapp.war"
          }
        }
      }
      // stage ('SonarQube'){
      //   steps{
      //     script{
      //       def mvnHome =  tool name: 'maven', type: 'maven'
      //       withSonarQubeEnv('sonar-pro') {
      //         sh "${mvnHome}/bin/mvn sonar:sonar"
      //       }
      //     }
      //   }
      // }
      stage('Docker Build') {
        steps{
          script{
            sh 'docker build -t kerajasekar/multi:v1 .'
            //sh 'docker images'
          }
        }
      }
 }
