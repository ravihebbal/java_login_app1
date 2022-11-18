pipeline{

    agent any

    stages {
        stage('git checkout'){

            steps{
                git 'https://github.com/ravihebbal/java_login_app1.git'
            }
        }

        stage('unit testing'){

            steps{
                sh "mvn clean test"
            }
        }

        stage('Integration testing'){

            steps{
                sh "mvn verify -DskipUnitTests"
            }
        }

        stage('maven build'){
            steps{
                sh "mvn clean install"
            }
        }

        stage('static code analysis'){
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'sonarqube-api-key') {
                    sh "mvn clean package sonar:sonar"
                    }
                }
            }
        }

        stage('Quality gate status'){
            steps{
                scripts{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-api-key'
                }
            }
        }

    }
}
