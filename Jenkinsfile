pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t java-docker-img:latest .' 
                sh 'docker tag java-docker-img lijisha27/java-maven-jenkins:latest'
                sh 'docker tag java-docker-img lijisha27/java-maven-jenkins:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "Mydockerhub-credential", url: "" ]) {
          sh  'docker push lijisha27/java-maven-jenkins:latest'
          sh  'docker push lijisha27/java-maven-jenkins:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 lijisha27/java-maven-jenkins"
 
            }
        }

    }
}