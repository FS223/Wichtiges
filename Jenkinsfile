pipeline {
    agent any

    environment {
        DOCKER_BUILDKIT = '1'
        JAVA_HOME = '/usr/lib/jvm/java-21-openjdk-amd64'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}
