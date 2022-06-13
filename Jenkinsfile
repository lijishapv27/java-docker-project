pipeline{
  agent any
  tools {
    maven 'maven'
    jdk 'Java'
  }
  environment {
    dockerhub=credentials('docker-credential')
  }
  stage('build image')
   {
    when{
      branch "prod"
    }
    steps{
      sh 'docker build -t maven-java-dockerfile .'
    }
   }
   stage('pushing to dockerhub')
   {
    when{
      branch "prod"
    }
    steps{
      sh 'docker tag java-docker-project lijisha27/java-maven-jenkins:latest '
      sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
      sh 'docker push lijisha27/java-maven-jenkins:latest '
    }
   }
}


