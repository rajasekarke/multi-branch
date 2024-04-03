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
      stage('Docker push'){
        steps{
          script{
              withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]){
              sh "docker login -u kerajasekar -p ${dockerPassword}"
              sh 'docker push kerajasekar/multi:v1'
              sh 'docker rmi kerajasekar/multi:v1'
            }
          }
        }
      }
    }
}

//       stage('Deploy on k8s') {    
//         steps {
//           script{
//             withKubeCredentials(kubectlCredentials: [[ credentialsId: 'kubernetes', namespace: 'ms' ]]) {
//                 sh 'kubectl apply -f kube.yaml'
//             }
//           }
//         }
//       }
//     }
// }
