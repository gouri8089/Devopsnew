pipeline {
    agent any

    environment {
        IMAGE_NAME = "welcome-react"
        CONTAINER_NAME = "welcome-react-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/gouri8089/GEEM.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker run -d -p 5173:5173 --name %CONTAINER_NAME% %IMAGE_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo 'React app deployed using Docker successfully 🎉'
        }
        failure {
            echo 'Deployment failed ❌'
        }
    }
}