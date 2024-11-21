pipeline {
    agent any
    stages {
        stage('Debug Environment') {
            steps {
                sh 'printenv'
            }
        }
        stage('Check Docker Version') {  // Changed name to make it unique
            steps {
                script {
                    sh '/usr/local/bin/docker --version'
                }
            }
        }
        stage('Clone Repository') {
            steps {
                git branch: 'dev', url: 'https://github.com/davidkairu/ci_cd_flask_app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh '/usr/local/bin/docker build -t flask-app .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh '/usr/local/bin/docker run -d -p 8080:5001 flask-app'
                }
            }
        }
    }
}
