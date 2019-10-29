pipeline {
    environment {
    registry = "sanmanivannan/jenkins-test"
    registryCredential = 'dockerhub-id'
  }
        agent any 
        stages {
            stage ('Packaging'){
                steps { 
                bat 'mvn clean package'
                      } 
            }
            stage ('Building Docker Image'){
                steps {
                //bat "docker build . -t webapp.${env.BUILD_ID}"
                bat "docker build . -t sanmanivannan/jenkins-test:${env.BUILD_ID}"
            } 
            }
            stage('Test') { 
                steps {
               echo 'test completed'
                 }
            }
            stage ('Pushing Docker Image to DockerHub'){
                steps {
                withCredentials([string(credentialsId: 'dhub', variable: 'dockerhub')]) {
                bat "docker login -u sanmanivannan -p ${dockerhub}"
                }
                bat 'docker push docker.io/sanmanivannan/jenkins-test'
            } 
            }
        }
}

