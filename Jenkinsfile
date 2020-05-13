<<<<<<< HEAD
pipeline {

    agent {label 'master'}
    stages{
=======
pipeline{
    agent any
    stages {
>>>>>>> 495292840df570635d5d72fb1d2181bdad1e4734
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
        agent {label 'linux_slave'}
        stage ('Deploy to Staging'){
            steps {
                build job:'deploy-to-QA'
            }
        }
        agent {label 'linux_slave'}
        stage ('Deploy to Production'){
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
