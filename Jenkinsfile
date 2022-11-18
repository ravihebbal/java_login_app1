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
                sh "mvn test"
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
    }
}
