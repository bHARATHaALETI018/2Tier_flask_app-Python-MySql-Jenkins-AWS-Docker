pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps {
                echo 'Cloning Repository'
                git branch: 'main', url:'https://github.com/bHARATHaALETI018/2Tier_flask_app-Python-MySql-Jenkins-AWS-Docker.git'
                echo 'Repository Cloned Successfully'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Image'
                sh 'docker build -t flask-mysql-app:v1.1 .'
                echo 'Image Built Successfully'
            }
        }
        stage('Pushing Image') {
            steps {
                echo 'Pushing Image to Docker Hub'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Application'
                sh 'docker compose up'
                echo 'Application Deployed Successfully'
            }
        }
    }
}
