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
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-api-key'
                }
            }
        }

        stage('upload war file to nexus'){
            steps{
                script{

                    def readPomVersion = readMavenPom file: 'pom.xml'

                    def nexusRepo = readPomVersion.version.endsWith("snapshot") ? "demoapp-snapshot" : "demoapp-release"
                    
                    nexusArtifactUploader artifacts: 
                    [
                        [artifactId: 'dptweb', 
                        classifier: '', 
                        file: 'target/login.war', 
                        type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus-auth', 
                    groupId: 'com.devopsrealtime', 
                    nexusUrl: '100.26.3.177:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demoapp-release', 
                    version: "${readPomVersion.version}"
                }
            }
            
        }

        stage('Docker image build'){
            steps{
                script{
                    sh "docker image build -t $JOB_NAME:v1.$BUILD_ID ."
                    sh "docker image tag $JOB_NAME:v1.$BUILD_ID ravihebbal/$JOB_NAME:v1.$BUILD_ID"
                    sh "docker image tag $JOB_NAME:v1.$BUILD_ID ravihebbal/$JOB_NAME:latest"
                    
                }
            }
        }

    }
}
