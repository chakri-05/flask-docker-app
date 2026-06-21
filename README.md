# Flask Docker CI/CD Pipeline

A simple Flask web application containerized with Docker and deployed through an automated Jenkins pipeline connected to GitHub.

## What this project demonstrates

- Writing a custom Dockerfile to containerize a Python Flask application
- Setting up Jenkins as a CI/CD automation server
- Connecting Jenkins to a GitHub repository for source control
- Automating build and deployment using Jenkins Freestyle jobs
- Debugging real infrastructure issues across permissions, networking, and Docker

## Tech stack

- Python 3.10 (Flask)
- Docker
- Jenkins
- Git / GitHub

## How it works

1. Code is pushed to this GitHub repository
2. Jenkins job pulls the latest code
3. Jenkins builds a Docker image using the Dockerfile
4. Jenkins stops the old container and deploys the new image
5. App becomes available on port 5050

## Problems solved during this build

- Jenkins user lacked permission to access project folder — fixed by relocating project into Jenkins' home directory with correct ownership
- Jenkins user lacked permission to access Docker socket — fixed by adding jenkins user to docker group
- Port mapping mismatch between Docker container and VirtualBox NAT port forwarding
- GitHub authentication required Personal Access Token instead of password
- Docker layer caching verified — confirmed only changed layers rebuild, unchanged layers reused

## Run locally

\`\`\`bash
docker build -t my-flask-app .
docker run -d -p 5050:5000 --name flaskcontainer my-flask-app
\`\`\`

Visit `http://localhost:5050`
