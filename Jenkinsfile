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

        stage('Shutdown existing containers') {
            steps {
                sh 'docker compose down'
            }
        }

        stage('Build Spring Boot Apps') {
            parallel {
                stage('Build Authentication Service') {
                    steps {
                        dir('authentication-service') {
                            sh 'chmod +x gradlew'
                            sh './gradlew build'
                        }
                    }
                }
                stage('Build Reports Service') {
                    steps {
                        dir('reports-service') {
                            sh 'chmod +x gradlew'
                            sh './gradlew build'
                        }
                    }
                }
            }
        }
        
        stage('Build React App') {
            steps {
                dir('apprenticonnect') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
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