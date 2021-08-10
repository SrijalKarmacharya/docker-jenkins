pipeline {
  agent any
  
  environment { 
        registry = "srijaldocker/pipe" 
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
  
  stages {
      
      
      stage('Checkout'){
           steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SrijalKarmacharya/docker-jenkins']]])
           }    
       }
       
        stage('check') {
            steps {
                echo 'done'
            }
        }
       
       stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage('Push Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')
                    }
                }
            }
        }
        
         // Running Docker container, make sure port 8096 is opened in 
        stage('Docker Run') {
            steps{
              script {
                 dockerImage.run("-p 8088:3000 --rm --name myNodeContainer2")
              }
            }
        }

        
        
       
   }
}    
