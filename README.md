# My App

A Node.js application deployed with Jenkins and Docker.

## Prerequisites
- Docker
- Jenkins
- Git

## Setup
1. Clone: `git clone https://github.com/Dhanashree-jadhav/my-app.git`
2. Build: `docker build -t my-app:latest .`
3. Run: `docker run -d -p 3000:3000 my-app:latest`
4. Access: `http://localhost:3000`

## CI/CD
- Automated with Jenkins pipeline at `http://localhost:8080/job/my-app-pipeline/`.