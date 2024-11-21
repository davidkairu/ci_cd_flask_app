pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'dev', url: 'https://github.com/davidkairu/ci_cd_flask_app.git'
            }
        }
        stage('Verify Docker Access') {
            steps {
                script {
                    sh '/usr/local/bin/docker --version'
                }
            }
        }
        stage('Verify Docker Access') {
            steps {
                script {
                    sh 'docker --version'
                }
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
