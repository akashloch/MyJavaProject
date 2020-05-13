pipeline{
    agent any
    node()
    stages {
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Build successful and archiving artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps {
                build job: 'deploy-to-QA'
            }
        }
        stage ('deploy to production'){
            steps{
                build job: 'deploy-to-prod'
            }
            post{
                success{
                    echo 'Code deployed to production'
                }
                failure{
                    echo 'Deployment failed'
                }
            }
        }

    }
}