pipeline{

    agent any

    stages {
        stage('git checkout'){

            steps{
                git 'https://github.com/ravihebbal/petclinic.git'
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

    }
}
