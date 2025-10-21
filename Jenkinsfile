pipeline {
    agent any

    environment {
        REGISTRY = "192.168.10.26:5000"
        IMAGE_NAME = "simple-app"
        VERSION = "v01"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "📦 Cloning repository..."
                git branch: 'main', url: 'https://github.com/rehanarrow26/simple-nodejs-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "🏗️ Building Docker image..."
                    sh """
                        docker build -t ${REGISTRY}/${IMAGE_NAME}:${VERSION} \
                                     -t ${REGISTRY}/${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Push to Local Registry') {
            steps {
                script {
                    echo "🚢 Pushing image to local registry..."
                    sh """
                        docker push ${REGISTRY}/${IMAGE_NAME}:${VERSION}
                        docker push ${REGISTRY}/${IMAGE_NAME}:latest
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build and push completed successfully!"
        }
        failure {
            echo "❌ Build or push failed. Please check logs."
        }
    }
}
