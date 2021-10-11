@Library('demo-maven') _
pipeline {
  agent any

  environment {
    AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
    AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
  } 

  tools {
    maven 'mvn-version'
  }

      stages {
          stage('Build') {
            steps {
                script{
                    welcome.buildMvn()
                }
            }
          }
    
        stage("Build image") {
            steps {
                script {
                    welcome.buildImageMvn()
                    sh "pwd"
                    sh "ls -lrt"
                }
            }
        }
    

      stage("Push image") {
        steps {
                script {
                    welcome.pushImageMvn()
               }
          }

          post {
                success {
                    archiveArtifacts 'target/*.jar'
                    sh 'aws configure set region us-east-1'
                    sh 'aws s3 cp ./target/springbootrestapiexample-11.jar s3://bucketname123321'
                }
            
      }
    }



//   stages {
//     stage('Build') {
//       steps {
//         sh 'mvn package'
//       }
//     }
    
//         stage("Build image") {
//             steps {
//                 script {
//                     echo "Build image with tag: ${env.BUILD_ID}"
//                     myapp = docker.build("alingavrila/ledger-service:${env.BUILD_ID}", "--build-arg VERSION='${env.BUILD_ID}' .")
//                 }
//             }
//         }
    

//       stage("Push image") {
//         steps {
//                 script {
//                     docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
//                             myapp.push("latest")
//                             myapp.push("${env.BUILD_ID}")
//                     }
//                }
//           }
//      }
//  }
  
}
