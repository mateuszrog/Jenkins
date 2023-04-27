pipeline {
    agent any
    environment {
        def BUILDVERSION = sh(script: "echo `date +%Y%m%d`", returnStdout: true).trim()
    }
    
    stages {
      stage("Awesome Stage") {
               steps {
                    echo "Current build version :: $(BUILDVERSION)_$(BUILD_NUMBER)"
               }
            }
        }
}
//   stage('Docker Build and Tag') {
//            steps {
              
//                 sh 'docker build -t nginxtest:latest .' 
//                 sh 'docker tag nginxtest 970922/nginxtest:latest'
//                 sh 'docker tag nginxtest 970922/nginxtest:$BUILDVERSION'
               
//           }
//         }
   
//   stage('Publish image to Docker Hub') {
          
//             steps {
//         withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
//           sh  'docker push 970922/nginxtest:latest'
//           sh  'docker push 970922/nginxtest:$BUILDVERSION' 
//         }
                  
//           }
//         }
     
//       stage('Run Docker container on Jenkins Agent') {
             
//             steps {
//                 sh "docker run -d -p 4030:80 970922/nginxtest"
 
//             }
//         }
//     }
// }
