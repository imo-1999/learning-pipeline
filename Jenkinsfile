pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Jar') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }

        stage('Debug Environment') {
            steps {
                sh '''
                    echo "PATH=$PATH"
                    which docker
                    which docker-credential-desktop
                    docker --version
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t learning-pipeline:1.0 .'
            }
        }

        stage('Verify Image') {
            steps {
                sh '/usr/local/bin/docker images'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}