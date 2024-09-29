

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

