pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Repository already checked out by Jenkins'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }
}