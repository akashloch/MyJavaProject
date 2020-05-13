
pipeline {

    agent {label 'master'}
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            agent{label 'linux_slave'}
            steps {
                build job:'deploy-to-QA'
            }
        }
        stage ('Deploy to Production'){
            agent{label 'linux_slave'}
            steps{
            
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }
    }
    
}
