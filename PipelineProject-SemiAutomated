pipeline {
    agent any 
        stages {
            stage ('Packaging'){
                steps {
                sh 'mvn clean package'
            } 
            post {
                success {
                    echo 'Now Archiving'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            } 
            }
        stage ('Deploy to Staging') {
            steps{
                build job: 'Deploy_Staging_8090'
            }

        }

        stage ('Deploy to Production'){
            steps{
            timeout(time: 5, unit: 'HOURS') {
                input message "Approve for Production"
            }
        
                build job: 'Deploy_to_Production'
            }
    
        }

        post{
            success{
                echo 'success'
            }

            failure{
                echo 'failure'
            }

        }
        
        }
}
                

