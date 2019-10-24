pipeline {
    agent any {
        stages {
            stage('Packaging')
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
            stage('Test')
                steps {
                echo 'Testing'
            }
            stage('deploy')
                steps {
                echo 'deploy'
            }
        }
                }
    }
}
