pipeline{
    agent {
        label 'DevServer'
    }

    environment {
        NAME = "Rahul"
    }

    tools {
        maven 'maven-build'
    }




    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }

    }
}