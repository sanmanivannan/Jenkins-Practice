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
                bat "docker build . -t webapp.${env.BUILD_ID}"
            } 
            }
            stage('Test') {
                steps {
               echo 'test completed'
                 }
            }
            stage ('Pushing Docker Image to DockerHub'){
                steps {
                bat 'docker login -u sanmanivannan -p santharam23'
                bat "docker push sanmanivannan/webapp.${env.BUILD_ID}"
            } 
            }
        }
}

