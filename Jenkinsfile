pipeline {
    agent any
    
tools 
{
    maven "M2_HOME"
}
    environment { 

        registry = "ihebdevops/achatproject" 

        registryCredential = 'docker_id' 

        dockerImage = '' 

    }

    stages {
         stage('GIT') {
            steps {
               echo 'bdina l git l git'
      //  sh " git url: 'https://github.com/ihebm123/GestionMagasinSpring.git' " 
              git branch:'main',url: 'https://github.com/ihebm123/TestMagasin.git'

         /*  sh "ls -lart " 
             sh "git branch -a"
             sh "git checkout branchname"*/
           
              echo 'foutna l git'
            }
         }
           stage('CLEAN') {
            steps {
              
          script {
   
               sh "mvn clean"
   
            }
   
        }
             }
             
                   stage('COMPILE') {
            steps {
              
          script {

               sh "mvn compile "

            }
  
        }
             }
        
              stage('TEST') {
            steps {

               sh "mvn test "

            }
              }
              
                    stage('jar') {
            steps {

               sh "mvn package "
               //sh 'docker container prune'//delet non actif containers container 

            }
              }
              
           /* stage("Building Docker Image") { 
             steps { 
                 script { 
                    
                    sh 'docker build -t achatproject/image:1.0 .'
                   
                 } 
             } 
         } 
         
         
           stage("Pushing Image to DockerHub") { 
             steps { 
                 script { 
                     withCredentials([usernamePassword(credentialsId: 'docker_id', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push achatproject/image:1.0'
                 } 
             } 
         } 
           }*/
           
        
        stage('Building Docker Image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":1.0" 

                }

            } 

        }

        stage('Pushing Image to DockerHub') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                      dockerImage.push() 

                    }

                } 

            }

        }
         
         
          /* stage('Cleaning Up Image') { 

            steps { 

                sh "docker rmi $registry:1.0" 

            }

        } */
         
         
          stage("Docker-Compose") { 
             steps { 
                 script { 
                    sh "docker-compose up   "
                 } 
             } 
         } 
              
              
              /* stage('NEXUS DEPLOY') {
            steps {

               sh "mvn deploy -Dmaven.test.skip=true "

            }

        }*/
        
           /*   stage('SONAR') {
            steps {
              
        
              sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar  "
     
           
              
            }
            
            
        }*/
        
    
}
}

