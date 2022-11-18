pipeline{

    agent any

    stages {
        stage('git checkout'){

            steps{
                git 'https://github.com/ravihebbal/java_login_app1.git'
            }
        }

  /*      stage('unit testing'){

            steps{
                sh "mvn clean test"
            }
        }

        stage('Integration testing'){

            steps{
                sh "mvn verify -DskipUnitTests"
            }
        }  */

    }
}
