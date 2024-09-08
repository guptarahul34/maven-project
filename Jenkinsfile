pipeline{
    agent {
        label 'DevServer'
    }

    environment {
        NAME = "Rahul"
    }

    tools {
        maven 'maven-build-demo'
    }




    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }

    }
}