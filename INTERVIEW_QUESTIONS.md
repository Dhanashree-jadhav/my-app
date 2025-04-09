# Jenkins Interview Questions and Answers

This document contains common interview questions about Jenkins and CI/CD, along with detailed answers to help with preparation. These are based on practical experience with a Node.js application deployed using Jenkins and Docker.

## 1. What is Jenkins, and how is it used in CI/CD?
- **Answer**: Jenkins is an open-source automation server widely used for Continuous Integration (CI) and Continuous Deployment/Delivery (CD). It helps automate the process of building, testing, and deploying software.
  - **CI**: Jenkins integrates code changes from multiple developers into a shared repository, running automated tests to catch issues early. For example, in my `my-app` project, Jenkins pulls code from GitHub, builds a Docker image, and tests it.
  - **CD**: It automates deployment to production-like environments. In my setup, Jenkins deploys the `my-app` container to localhost:3000 after a successful build.
  - **How It Works**: Jenkins uses plugins (e.g., Git, Docker) and pipelines (defined in a `Jenkinsfile`) to orchestrate these tasks. It runs on a server (e.g., a Docker container in my case) and can be triggered manually or by code commits.

## 2. What is a Jenkinsfile?
- **Answer**: A `Jenkinsfile` is a text file that contains the definition of a Jenkins pipeline using a domain-specific language (DSL) based on Groovy. It allows you to codify the CI/CD process in version control (e.g., GitHub).
  - **Purpose**: It specifies stages like build, test, and deploy, making the pipeline reusable and versioned. In my `my-app` project, the `Jenkinsfile` defines steps to build a Docker image, run tests (placeholder), and deploy the app.
  - **Types**:
    - **Declarative**: Structured, easier to read (e.g., `pipeline { agent any; stages { ... } }`).
    - **Scripted**: More flexible, uses Groovy scripting.
  - **Benefit**: Keeps the pipeline configuration with the codebase, enabling collaboration and consistency.

## 3. How do you create and configure Jenkins pipelines?
- **Answer**: Creating and configuring a Jenkins pipeline involves several steps:
  1. **Install Jenkins**: Set it up on a server or Docker container (e.g., `docker run -d --name jenkins ...` as in my setup).
  2. **Create a Pipeline Job**:
     - In the Jenkins UI (`http://localhost:8080`), click "New Item," name it (e.g., `my-app-pipeline`), and choose "Pipeline."
     - Configure the SCM (e.g., Git with `https://github.com/Dhanashree-jadhav/my-app.git`).
  3. **Write a Jenkinsfile**:
     - Define stages (e.g., build, test, deploy) in the project root.
     - Example from my project:
       ```groovy
       pipeline {
           agent any
           stages {
               stage('Build') {
                   steps {
                       sh 'docker build -t my-app:latest .'
                   }
               }
               stage('Deploy') {
                   steps {
                       sh 'docker run -d --name my-app -p 3000:3000 my-app:latest'
                   }
               }
           }
       }

    4    What are some common stages in a Jenkins pipeline?
          <br>
        Answer: A Jenkins pipeline typically includes the following stages, depending on the project:
  <br>
        Checkout: Pulls code from the repository (e.g., GitHub).
   <br>
        Build: Compiles or packages the application (e.g., docker build for my my-app).
   <br>
        Test: Runs unit, integration, or end-to-end tests (e.g., npm test if configured).
   <br>
        Deploy: Deploys the artifact to a server or container (e.g., docker run for my app on port 3000).
   <br>
        Cleanup: Removes temporary files or stops old containers (e.g., docker rm in my setup).
   <br>
        Notify: Sends success/failure notifications (e.g., via email or Slack).
   <br>
        Example: My my-app pipeline includes Build and Deploy stages, with Cleanup planned as an enhancement.
   <br>
    
    
    
    5   What is the difference between a declarative and scripted Jenkins pipeline?
  <br>
        Declarative Pipeline:
            Structure: Uses a predefined structure with blocks like pipeline, agent, stages, and steps.
            Syntax: More concise and readable, ideal for beginners.
  <br>
            Example:
                pipeline {
                    agent any
                    stages {
                        stage('Build') {
                            steps {
                                echo 'Building...'
                            }
                        }
                    }
                }         
        Advantages: Easier to maintain, supports visual editing in Jenkins Blue Ocean.
  <br>
        Scripted Pipeline:
            Structure: More flexible, written in Groovy with imperative programming.
            Syntax: Allows complex logic (e.g., loops, conditionals).
  <br>
            Example:
                    node {
                        stage('Build') {
                            sh 'echo Building...'
                        }
                    }
  <br>
        Advantages: Greater control, useful for advanced workflows.
        Key Difference: Declarative is structured and opinionated, while Scripted is flexible but requires more Groovy knowledge. My my-app uses declarative for simplicity.
