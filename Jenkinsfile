pipeline {
    agent any
    environment {
        def BUILDVERSION = sh(script: "echo `date +%Y%m%d`", returnStdout: true).trim()
        def BUILDFULLNAME = "${BUILDVERSION}_${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Full Name Stage') {
               steps {

                   sh 'echo "Current build version :: ${BUILDFULLNAME}"'
                   sh '${BUILDFULLNAME} > .env'

               }
        }

        stage('Docker Build and Tag for Ubuntu') {
               steps {
                    sh 'cd ubuntu_docker'
                    sh 'docker build -t ubuntu_devops:latest .' 
                    sh 'docker tag ubuntu_devops 970922/ubuntu_devops:latest'
                    sh 'docker tag ubuntu_devops 970922/ubuntu_devops:${BUILDFULLNAME}'

               }
        }

        stage('Publish Ubuntu image to Docker Hub') {

                steps {
          
                    withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                    sh  'docker push 970922/ubuntu_devops:latest'
                    sh  'docker push 970922/ubuntu_devops:${BUILDFULLNAME}' 
                    
                    }
                }
        }

        stage('Run Docker container on Jenkins Agent') {

                steps {
                    
                    sh "docker run -d -p 4030:80 970922/ubuntu_devops"
                
                }
        }
    }
}
