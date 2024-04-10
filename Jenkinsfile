pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from Git
                git 'https://github.com/yourusername/your-repo.git'
            }
        }
        stage('Build and Test Frontend') {
            steps {
                // Build and test your frontend
                sh 'cd frontend && npm install && npm run test'
            }
        }
        stage('Build and Test Backend') {
            steps {
                // Build and test your backend
                sh 'cd backend && npm install && npm run test'
            }
        }
        stage('Dockerize') {
            steps {
                // Build Docker images for frontend and backend
                script {
                    docker.build('frontend-image', './frontend')
                    docker.build('backend-image', './backend')
                }
            }
        }
        stage('Deploy') {
            steps {
                // Push Docker images to a Docker registry
                script {
                    docker.withRegistry('https://your-docker-registry', 'your-registry-credentials') {
                        docker.image('frontend-image').push()
                        docker.image('backend-image').push()
                    }
                }
                // Deploy the application (e.g., using Docker Compose or Kubernetes)
                sh 'docker-compose up -d' // Example for Docker Compose
            }
        }
    }
}
