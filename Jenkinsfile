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
      sh 'docker tag java-docker-project lijisha27/java-docker-project:1.0 '
      sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
      sh 'docker push lijisha27/java-dockder-project:1.0 '
    }
   }
}


