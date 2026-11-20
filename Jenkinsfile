pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps {
                echo 'Cloning Repository'
                git branch: 'main', url:'https://github.com/ShaftainAli/2Tier_flask_docker.git'
                echo 'Repository Cloned Successfully'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Image'
                sh 'docker build -t flask-app:latest .'
                echo 'Image Built Successfully'
            }
        }
        stage('Pushing Image') {
            steps {
                echo 'Pushing Image to Docker Hub. Here i did not really push image, but you can push and change the name of the image in docker-compose file and continue . . .'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying Application'
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
                echo 'Application Deployed Successfully'
            }
        }
    }
}
