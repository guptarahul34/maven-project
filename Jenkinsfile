pipeline{
    agent {
        label 'DevServer'
    }

    parameters {
        choice choices: ['dev', 'prod'], name: 'select_environment'
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
                stage('Test-A'){
                    agent { label 'DevServer' }
                    steps{
                        echo "This is stage Test-A"
                        sh 'mvn test'
                    }
                }

                stage('Test-B'){
                    agent { label 'DevServer' }
                    steps{
                        echo "This is stage Test-B"
                        sh 'mvn test'
                    }
                }
            }
            post {
                success {
                    dir('webapp/target'){
                        stash includes: '*.war', name: 'maven-stash'
                    }
                //archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy_Dev'){
            when { expression {params.select_environment == 'dev'}
                beforeAgent true }
            //agent { label 'DevServer' }
            steps{
                dir('/var/www/html'){
                    unstash 'maven-stash'
                }
                sh '''
                    cd /var/www/html
                    jar -xvf webapp.war
                '''
            }
        }

    }
}