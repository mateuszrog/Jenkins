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
                    sh 'echo "BUILDFULLNAME=${BUILDFULLNAME}" > .env'

               }
        }

        stage('Docker Compose Pull and Build') {
               steps {
                    
                    sh 'docker-compose build --pull' 

               }
        }

        stage('Publish images to Docker Hub') {

                steps {
          
                    withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                    sh  'docker-compose push'
                    
                    }
                }
        }

        stage('Run Docker containers on Jenkins Agents') {

                steps {
                    
                    sh "docker run -d -p 4030:80 970922/centos"
                    sh "docker run -d -p 4040:80 970922/ubuntu"
                    sh "docker run -d -p 4050:80 970922/nginx"

                
                }
        }
    }
}
