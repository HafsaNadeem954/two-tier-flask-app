pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Jenkins automatically checks out the code from the Git URL configured in the job.
                echo "Repository code successfully checked out."
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Builds the Docker image based on the Dockerfile found in the workspace.
                sh 'docker build -t flask-app-image .'
            }
        }
        
        stage('Run Containers (Deploy)') {
            steps {
                echo "Deploying the two-tier application using Docker Compose..."
                // Use 'docker compose down' to stop and remove previous containers gracefully
                sh 'docker compose down --remove-orphans || true'
                
                // Start the database and the Flask application in detached mode
                sh 'docker compose up -d'
                
                // Print running containers for verification
                sh 'docker ps -a'
            }
        }
    }

    post {
        always {
            // Cleans up the Jenkins workspace directory after every build.
            cleanWs()
        }
        success {
            echo "Pipeline finished successfully. The application is now live at http://51.21.248.38:5000"
        }
        failure {
            echo "Pipeline FAILED. Check console output for specific Docker or Groovy errors."
        }
    }
}
