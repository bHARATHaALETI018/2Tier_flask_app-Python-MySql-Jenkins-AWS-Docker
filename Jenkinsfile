pipeline {
    agent any
    
    options {
        timeout(time: 10, unit: 'MINUTES')
        retry(2)
    }

    stages {
        stage('Git Clone') {
            steps {
                echo 'Cloning Repository'
                git branch: 'main', url:'https://github.com/bHARATHaALETI018/2Tier_flask_app-Python-MySql-Jenkins-AWS-Docker.git'
                echo 'Repository Cloned Successfully'
            }
        }
        
        stage('Cleanup') {
            steps {
                echo 'Cleaning up old containers and images'
                sh '''
                    # Stop and remove containers
                    docker compose down --remove-orphans || true
                    
                    # Remove old images to free space
                    docker image prune -f || true
                    
                    # Remove unused volumes
                    docker volume prune -f || true
                '''
                echo 'Cleanup completed'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building Image'
                timeout(time: 5, unit: 'MINUTES') {
                    sh 'docker build -t flask-mysql-app:v1.1 .'
                }
                echo 'Image Built Successfully'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying Application'
                timeout(time: 3, unit: 'MINUTES') {
                    sh '''
                        # Ensure clean deployment
                        docker compose down --remove-orphans || true
                        
                        # Wait a moment for cleanup
                        sleep 5
                        
                        # Deploy with resource limits
                        docker compose up -d --build --force-recreate
                        
                        # Wait for containers to be ready
                        sleep 10
                        
                        # Verify deployment
                        docker compose ps
                    '''
                }
                echo 'Application Deployed Successfully'
            }
        }
        
        stage('Health Check') {
            steps {
                echo 'Performing health check'
                timeout(time: 2, unit: 'MINUTES') {
                    sh '''
                        # Wait for application to be ready
                        for i in {1..30}; do
                            if curl -f http://localhost:5000 >/dev/null 2>&1; then
                                echo "Application is healthy"
                                exit 0
                            fi
                            echo "Waiting for application... ($i/30)"
                            sleep 2
                        done
                        echo "Health check failed"
                        exit 1
                    '''
                }
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed - cleaning up'
            sh 'docker compose down --remove-orphans || true'
        }
        always {
            echo 'Pipeline completed'
            sh 'docker system df || true'
        }
    }
}