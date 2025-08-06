// Declarative Pipeline
pipeline {
    // Agent 'any' means Jenkins can use any available agent/node to run this pipeline.
    agent any

    // Environment variables available to all stages
    environment {
        // Use the GitHub repository name for the Docker image and container name
        // This makes it easy to identify resources.
        IMAGE_NAME = "omdalvi070205/todo-list-app-cicd"
        CONTAINER_NAME = "django-todo-app"
    }

    // The sequence of stages to execute for the CI/CD process
    stages {
        // STAGE 1: Build the Docker Image
        stage('Build') {
            steps {
                script {
                    echo "--- Building the Docker image ---"
                    // The 'docker.build' command builds an image from the Dockerfile
                    // in the current directory and tags it with the name defined above.
                    def customImage = docker.build(IMAGE_NAME)
                }
            }
        }

        // STAGE 2: Run Tests (Placeholder)
        // This is a crucial stage in a real-world pipeline.
        stage('Test') {
            steps {
                script {
                    // For now, this is a placeholder. In a real project, you would
                    // run your unit tests or integration tests here.
                    // Example: sh 'docker run --rm ${IMAGE_NAME} python manage.py test'
                    echo "--- Testing stage (skipping for now) ---"
                }
            }
        }

        // STAGE 3: Deploy the Application
        stage('Deploy') {
            steps {
                script {
                    echo "--- Deploying the container ---"

                    // Stop and remove any old container with the same name to avoid conflicts.
                    // '|| true' ensures the command doesn't fail if the container doesn't exist.
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"

                    // Run the new container from the image we just built.
                    // -d: detached mode (runs in the background)
                    // -p: maps port 8000 on the host to port 8000 in the container
                    // --name: assigns a name to the container for easy management
                    sh "docker run -d -p 8000:8000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }

    // Post-build actions that run regardless of the pipeline's success or failure
    post {
        always {
            echo "--- Pipeline finished. Cleaning up old Docker images... ---"
            // This is a good practice to prevent the server from running out of disk space.
            // It removes any dangling Docker images (images without a tag).
            sh 'docker image prune -f'
        }
    }
}
