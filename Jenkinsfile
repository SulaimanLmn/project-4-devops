pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/SulaimanLmn/project-4-devops.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile from the cloned repo
                    sh 'docker build -t project-4-image .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any previous container with the same name
                    sh 'docker stop project-4-container || true'
                    sh 'docker rm project-4-container || true'

                    // Run a new container from the built image
                    sh 'docker run --rm -d --name project-4-container -p 8081:80 project-4-image'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
