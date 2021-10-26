pipeline {   
    agent any  
    environment{     
        dockerImage=""     
        registry="thanu123456/jenkinsimage"   
        registryCredential = "dockerHub"  
        }   
        stages {    
            stage('Checkout') {   
                steps {          
                   checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/thanujaa-vb/ci_cd-pipeline.git']]])      
                    }    
                    }    
                    stage("build Docker image"){     
                        steps{              
                            script{         
                                dockerImage = docker.build registry     
                                }         
                                }
                                }
                                stage("upload Docker image"){  
                                    steps{              
                                        script{         
                                            docker.withRegistry( '', registryCredential ) { 
                                                dockerImage.push()               
                                                }            
                                           }        
                                    }      
                               }      
                               stage('docker stop container') {  
                                       steps {           
                                              bat 'docker ps -f name=jenkinsImageContainer '        
                                              bat 'docker container ls -a -fname=jenkinsImageContainer'     
                                             }       
                                        }       
                                stage('Docker Run') { 
                                       steps{           
                                              script {     
                                                     dockerImage.run("-p 3000:3000 --rm --name jenkinsImageContainer") 
                                                        }     
                                                    }     
                                           }   
        }
}
