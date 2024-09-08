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
                sh 'mvn clean package -Dmaven.clean.skip=true'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }

        stage('Test'){
            parallel{
                stage('Test1'){
                    steps{
                        echo "This is stage test1"
                    }
                }

                stage('Test2'){
                    steps{
                        echo "This is stage test2"
                    }
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

    }
}