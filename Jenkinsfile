pipeline{
    environment{
        registry = "ellande/helloworld"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    
    agent any
    
    stages{
        stage('GitCheckout'){
            steps{
                checkout scm
            }
        }
        stage('Building image'){
            steps{
                dir('app'){
                    script{
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }
        }
        stage('Publishing Image'){
            steps{
                script{
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        dockerImage("latest")
                    }
                    echo "trying to push Docker Build to DockerHub"    
                }
            }
        }
        stage('Remove Unused docker image'){
            steps{
                bat 'docker rmi $registry:$BUILD_NUMBER'
            }
        }
    }
}
