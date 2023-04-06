pipeline {

    agent any

    stages {
        stage('GIT Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/rohin079/sme-2.git'
            }
        }

        stage('UNIT TESTING') {
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TESTING') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage('BUILD') {
            steps {
                sh 'mvn clean install'
            }
        }

         stage('STATIC CODE ANALYSIS') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'tokenid') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        // stage('QUALITY GATE STATUS') {
        //     steps {
        //         script {
        //             waitForQualityGate abortPipeline: false, credentialsId: 'tokenid'
        //         }
        //     }
        // }

         stage('Upload Artifacts to Nexus'){
            
            steps{

                script{

                nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/UPES.jar', type: 'jar']], credentialsId: 'nexuscreds', groupId: 'com.example', nexusUrl: 'http://13.50.233.31:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'java-release', version: '1.0.0'
                }
            }
        }
    }
}
