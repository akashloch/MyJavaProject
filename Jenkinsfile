pipeline{
    agent any{
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
        }

    }
}