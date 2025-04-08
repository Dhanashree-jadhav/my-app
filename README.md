# My App

A simple Node.js application deployed with Jenkins and Docker.

## Setup
1. Clone the repo: `git clone https://github.com/Dhanashree-jadhav/my-app.git`
2. Build the Docker image: `docker build -t my-app:latest .`
3. Run the container: `docker run -d -p 3000:3000 my-app:latest`
4. Access at `http://localhost:3000`

## CI/CD
- Jenkins pipeline automates build and deploy.