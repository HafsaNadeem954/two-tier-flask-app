pipeline{
    
    agent any;
    
    stages{
        stage("Code Clone"){
            steps{
                script{
                    // Note: This uses a hardcoded clone step. It's usually better to use Jenkins' built-in SCM checkout
                    // but since you used the pipeline script from SCM, the code is already checked out to the workspace.
                    // This specific 'clone' line might not be necessary or might need to be adjusted to a proper git checkout step.
                    // For now, let's proceed without the manual clone step since Jenkins does it automatically.
                }
            }
        }
        stage("Trivy File System Scan"){
            steps{
                script{
                    // Assuming trivy_fs() is defined in a shared library or environment, we must remove it if it's not available.
                    // If you don't have the Trivy plugin or a custom step, this will fail. Let's comment out the body for now.
                    echo "Skipping Trivy scan as shared library function is missing."
                }
            }
        }
        stage("Build"){
            steps{
                // This command will build the image from the Dockerfile in the current workspace.
                sh "docker build -t two-tier-flask-app ."
            }
            
        }
        stage("Test"){
            steps{
                echo "Developer / Tester tests likh ke dega..."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                script{
                    // WARNING: This step will fail unless you have a Docker Hub credential set up in Jenkins
                    // with the ID 'dockerHubCreds' and the 'docker_push' function is available.
                    echo "Skipping Docker Push to avoid credential failure."
                    // docker_push("dockerHubCreds","two-tier-flask-app")
                }  
            }
        }
        stage("Deploy"){
            steps{
                // Note: The Docker Compose up command requires the 'docker-compose.yml' file to be in the repository root.
                sh "docker compose up -d --build flask-app"
            }
        }
    }

    post{
        // WARNING: This section requires the 'Email Extension Plugin' and configuration, which may not be set up yet.
        success{
            echo "Build successful. Skipping email notification."
        }
        failure{
            echo "Build failed. Skipping email notification."
        }
    }
}
