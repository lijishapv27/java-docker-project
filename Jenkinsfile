pipeline { 

    environment { 
        

        registry = "lijisha27/java-maven-jenkins" 

        registryCredential = 'Mydockerhub-credential' 

        dockerImage = ' ' 

    }

    agent {
        dockerfile true
    } 

    stages { 

        stage('Cloning our Git') { 

            steps { 
                git branch: 'main', url: 'https://github.com/lijishapv27/java-docker-project.git'


            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 

        stage('Cleaning up') { 

            steps { 

                sh "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

    }

}
