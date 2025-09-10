pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "jeevankumar100/ecommerce"
        DOCKER_CONTAINER = "ecommerce_app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/JeevanKumar100/E-Commerce.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop & remove old container if running
                    sh '''
                    docker ps -q --filter "name=$DOCKER_CONTAINER" | grep -q . && docker stop $DOCKER_CONTAINER && docker rm $DOCKER_CONTAINER || true
                    docker run -d --name $DOCKER_CONTAINER -p 3000:3000 $DOCKER_IMAGE
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! App is running on port 3000"
        }
        failure {
            echo "❌ Build/Deployment failed"
        }
    }
}
