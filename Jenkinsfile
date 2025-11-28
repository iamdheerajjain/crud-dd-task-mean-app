pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        VM_HOST = credentials('vm_host')
        VM_USERNAME = credentials('vm_username')
        VM_SSH_KEY = credentials('vm_ssh_key')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Backend Tests') {
            steps {
                script {
                    sh '''
                        cd backend
                        npm install
                        # Add backend tests here if you have any
                        echo "Backend tests would run here"
                    '''
                }
            }
        }
        
        stage('Frontend Tests') {
            steps {
                script {
                    sh '''
                        cd frontend
                        npm install
                        # Add frontend tests here if you have any
                        echo "Frontend tests would run here"
                    '''
                }
            }
        }
        
        stage('Build Backend Image') {
            steps {
                script {
                    docker.build("mean-backend:${env.BUILD_NUMBER}", './backend')
                }
            }
        }
        
        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build("mean-frontend:${env.BUILD_NUMBER}", './frontend')
                }
            }
        }
        
        stage('Push Backend Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        docker.build("${DOCKERHUB_CREDENTIALS_USR}/mean-backend:latest", './backend').push()
                    }
                }
            }
        }
        
        stage('Push Frontend Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        docker.build("${DOCKERHUB_CREDENTIALS_USR}/mean-frontend:latest", './frontend').push()
                    }
                }
            }
        }
        
        stage('Deploy to VM') {
            steps {
                script {
                    sh '''
                        echo "Deploying to VM..."
                        ssh -o StrictHostKeyChecking=no -i $VM_SSH_KEY $VM_USERNAME@$VM_HOST \
                            "cd /home/prakuljain/crud-dd-task-mean-app && \
                             echo 'Pulling latest images...' && \
                             docker pull ${DOCKERHUB_CREDENTIALS_USR}/mean-backend:latest && \
                             docker pull ${DOCKERHUB_CREDENTIALS_USR}/mean-frontend:latest && \
                             echo 'Stopping existing containers...' && \
                             docker-compose down && \
                             echo 'Starting new containers...' && \
                             docker-compose up -d"
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            cleanWs()
        }
    }
}