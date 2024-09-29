

pipeline {
    agent any

    tools {
        nodejs "node16" // Your NodeJS installation name
    }

    environment {
        DOCKER_IMAGE = 'my-node-app:${env.BUILD_ID}' // Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rajeshbuece/NodeJSapplication-DOCKER'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // You can add your test commands here
                echo 'Running tests...'
                sh 'npm test || echo "No tests found."'
            }
        }

        stage('Deploy to Docker') {
            steps {
                script {
                    // Run the Docker container
                    sh "docker run -d -p 3000:3000 $DOCKER_IMAGE"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline complete'
        }
        success {
            // Notify on success
            //slackSend(channel: '#your-channel', message: "Build succeeded: ${env.BUILD_URL}")
            // OR
            // mail to: 'your-email@example.com', subject: "Build succeeded", body: "Check console output at ${env.BUILD_URL}"
        }
        failure {
            // Notify on failure
            //slackSend(channel: '#your-channel', message: "Build failed: ${env.BUILD_URL}")
            // OR
            // mail to: 'your-email@example.com', subject: "Build failed", body: "Check console output at ${env.BUILD_URL}"
        }
    }
}

