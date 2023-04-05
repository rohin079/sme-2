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
    }
}
