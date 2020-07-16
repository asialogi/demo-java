pipeline {
    tools {
  maven 'sgh'
  git 'Default'
  jdk 'sgh-jdk'
            }
    agent any 
    stages { 
 /*       stage ('SCM') { 
            steps { 
                git 'https://github.com/asialogi/demo-java.git'
                }   
            }*/
        stage ('Compiling') { 
            steps { 
                  sh 'mvn clean compile'
                }   
            }
        stage ('Packaging') {
            steps { 
                 sh 'mvn clean package'
                 }
            }
        stage ('CodeQualityCheck') {
            steps {
               withSonarQubeEnv( installationName: 'sgh-code-scanning') {
               sh 'mvn clean sonar:sonar'
                } }
            }

            }        
         post {  
          success {  
             mail bcc: '', body: "<b>Jenkins Job Status</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "Successful CI: Project name -> ${env.JOB_NAME}", to: "pponnam@ap.logicalis.com";  
         }  
          failure {  
             mail bcc: '', body: "<b>Jenkins Job Status</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "pponnam@ap.logicalis.com";  
         }  
          unstable {  
             mail bcc: '', body: "<b>Jenkins Job Status</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "Unstable CI: Project name -> ${env.JOB_NAME}", to: "pponnam@ap.logicalis.com";  
         }  
          changed {  
            mail bcc: '', body: "<b>Jenkins Job Status</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "Changed from unstable to stable CI: Project name -> ${env.JOB_NAME}", to: "pponnam@ap.logicalis.com";  
         }  
     }  
    }