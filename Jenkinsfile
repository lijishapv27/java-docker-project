pipeline { 

    environment { 
        imagename = "java-dockder-project"

        registry = "lijisha27/java-maven-jenkins" 

        registryCredential = 'docker-credential' 

        dockerImage = '' 

    }

    agent any 
        
        stages { 

        stage('Docker node test') {
                agent {
                        docker {
                        // Set both label and image
                        label 'docker'
                        image 'node:7-alpine'
                        args '--name docker-node' // list any args
                        }
                }
                steps {
                        // Steps run in node:7-alpine docker container on docker agent
                        sh 'node --version'
                }
        }

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
