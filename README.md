# ToDo-list-app-CICD
A simple todo app built with django
<img width="2880" height="1568" alt="image" src="https://github.com/user-attachments/assets/7aa30d59-909c-416d-aecb-f903935beadb" />
Django ToDo List App with CI/CD Pipeline
This repository contains a simple ToDo List web application built with Django. It is configured with a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins and Docker to automate the build, test, and deployment processes.

CI/CD Pipeline Overview
This project uses a "Pipeline as Code" methodology, where the entire deployment workflow is defined in a Jenkinsfile. When new code is pushed to the main branch on GitHub, a webhook triggers the Jenkins pipeline, which automatically executes the following stages:

Build: Jenkins checks out the latest code and uses the Dockerfile to build a new, versioned Docker image of the application.

Test: (Placeholder Stage) This stage is reserved for running automated tests (e.g., unit tests, integration tests) to ensure code quality and prevent regressions.

Deploy: If the build is successful, Jenkins deploys the application by stopping the old Docker container and running a new container from the newly built image.

Prerequisites
Before you begin, ensure you have the following set up:

A Server: An EC2 instance (Ubuntu 22.04 or later is recommended) or any other cloud/local server.

Jenkins: A running Jenkins instance accessible via a public IP or domain.

Docker: Docker must be installed on the same server where Jenkins is running.

GitHub Account: To host the repository and configure webhooks.

🚀 Setup and Configuration
Follow these steps to get the automated pipeline running.

Step 1: Server Setup
Connect to your server via SSH and install Docker.

# Update package lists
sudo apt-get update

# Install Docker
sudo apt-get install -y docker.io

# Add the 'jenkins' user to the 'docker' group
# This is CRUCIAL to allow Jenkins to execute Docker commands.
sudo usermod -aG docker jenkins

# Apply the group changes by restarting the Jenkins service
sudo systemctl restart jenkins

Step 2: Jenkins Configuration
Install Required Plugins:

From your Jenkins dashboard, go to Manage Jenkins > Plugins.

Install the following plugins: Docker Pipeline and GitHub Integration.

Create the Pipeline Job:

On the Jenkins dashboard, click New Item.

Enter a name for your project (e.g., django-todo-cicd).

Select Pipeline and click OK.

Configure the Pipeline:

In the General section, check the GitHub project box and enter your repository URL (e.g., https://github.com/Omdalvi070205/ToDo-list-app-CICD).

In the Build Triggers section, check GitHub hook trigger for GITScm polling. This tells Jenkins to listen for webhook events from GitHub.

In the Pipeline section:

Choose Pipeline script from SCM.

SCM: Select Git.

Repository URL: Enter your repository URL (e.g., https://github.com/Omdalvi070205/ToDo-list-app-CICD.git).

Branch Specifier: Ensure it is set to */main or */master depending on your primary branch.

Script Path: Keep the default, which is Jenkinsfile.

Save the pipeline configuration.

Step 3: GitHub Webhook Configuration
In your GitHub repository, go to Settings > Webhooks.

Click Add webhook.

Payload URL: Enter your Jenkins environment URL, followed by /github-webhook/. For example: http://<your-jenkins-ip>:8080/github-webhook/

Content type: Select application/json.

Click Add webhook. You should see a green checkmark next to it if the connection is successful.

How It Works
Commit Code: Make a change to the application code and push it to the main branch on GitHub.

Trigger: The push event fires the webhook, notifying Jenkins.

Execute: Jenkins automatically starts the pipeline, pulling the latest code.

Deploy: The Jenkinsfile runs through the build and deploy stages, and your updated application will be live on your server within minutes.

You can view the live application at 
### http://54.210.38.136:8000.


