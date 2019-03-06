pipeline {
  environment {
     registry = "arkakundu1407/docker-pipeline"
     registryCredential = 'dockerhub'
     dockerImage = ''
     containerId = sh(script: 'docker ps -aqf "name=node-app"',returnStdout: true)
   }
   agent any
   tools {nodejs "node"}
   
   stages {
     
       stage('Cloning git') {
         steps {
            git 'https://github.com/arkakundu1407/node-todo-frontend.git/'
          }
        }
        stage('Build') {
           steps {
             sh 'npm install'
           }
         }
       stage('Test') {
         steps {
             sh 'npm test'
             }
           }  
           
       stage('Building Image') {
         steps {
           script {
             dockerImage = docker.build registry + ":$BUILD_NUMBER"
             }
          }
       }
     stage('Push Image') {
       steps{
         script{
           docker.withRegistry('',registryCredential) {
             dockerImage.push()
         }
        }
      }
     }
    
   }
 }
        
