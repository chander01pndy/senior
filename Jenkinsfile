pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:latest .' 
                  sh 'docker tag nginxtest chanderpndy01/nginxtest:latest'
                sh 'docker tag nginxtest chanderpndy01/nginxtest:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker_hub_login", url: "" ]) {
          sh  'docker push chanderpndy01/nginxtest:latest'
          sh  'docker push chanderpndy01/nginxtest:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 chanderpndy01/nginxtest"
 
            }
        }
             
 
           
        }
    }
}
