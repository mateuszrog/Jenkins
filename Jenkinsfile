pipeline {
    agent any
    environment {
        def BUILDVERSION = sh(script: "echo `date +%Y%m%d`", returnStdout: true).trim()
        def BUILDFULLNAME = "${BUILDVERSION}_${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Full Name Stage') {
               steps {
                   echo "Current build version :: ${BUILDFULLNAME}"
               }
        }

        stage('Docker Build and Tag') {
               steps {

                    sh 'docker build -t nginxtest:latest .' 
                    sh 'docker tag nginxtest 970922/nginxtest:latest'
                    sh 'docker tag nginxtest 970922/nginxtest:${BUILDFULLNAME}'
               }
        }

        stage('Publish image to Docker Hub') {

                steps {
          
                    withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                    sh  'docker push 970922/nginxtest:latest'
                    sh  'docker push 970922/nginxtest:${BUILDFULLNAME}' 
                    
                    }
                }
        }

        stage('Run Docker container on Jenkins Agent') {

                steps {
                    
                    sh "docker run -d -p 4030:80 970922/nginxtest"
                
                }
        }
    }
}
