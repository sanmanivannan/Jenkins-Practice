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
             stage ('Run Docker Container from DockerHub Image'){
                 steps {
                   def dockerrun = 'docker run -p 8080:8080 -d --name my-app sanmanivannan/jenkins-test:latest'
                                                          // bat 'ssh -i secret*.pem user@<awsec2instance-Ip>'
                    sshagent(['ec2-user']) {         //enter the credential details on the sshAgent Plugin
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.36.230 ${dockerrun}"
 }
           }
        }
}
}
