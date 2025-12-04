pipeline {
    agent any
       tools {
        maven 'Maven3'   // must match the name in Jenkins config
        jdk 'Java17'     // must match the name in Jenkins config
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
