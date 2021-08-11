pipeline {
  agent any
  
  environment { 
        registry = "srijaldocker/pipe1" 
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
       
      stage('Build & Push Image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage = docker.build registry
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')
                    }
                }
            }
        }
        
        
       
   }
}    
