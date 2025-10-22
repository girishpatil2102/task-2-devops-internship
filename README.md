🚀 Task 2 – CI/CD Pipeline using Jenkins
👨‍💻 Task Overview

This project demonstrates the implementation of a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins, Docker, and GitHub Webhooks.
The pipeline automates the process of fetching code from GitHub, building and testing it using Jenkins, and packaging the application inside a Docker container — all triggered automatically upon every GitHub commit or push.

🧩 Tech Stack

Source Code Management: Git & GitHub

CI/CD Tool: Jenkins

Containerization: Docker

Tunneling: Ngrok

Language/Framework: Node.js

OS/Environment: Windows 10

⚙️ Pipeline Flow

GitHub Push → Jenkins Webhook Trigger → Build → Test → Docker Build → Deployment

Stages:

Checkout – Jenkins pulls the latest code from GitHub.

Build – Installs dependencies via npm install.

Test – Runs automated tests (npm test).

Deploy – Builds the Docker image for the Node.js app.

🧱 Steps Performed
1️⃣ Install Required Tools

Installed and configured:

Git

Node.js & npm

Docker Desktop

Jenkins

Ngrok (for tunneling local Jenkins to GitHub)

2️⃣ Configure Jenkins

Open Jenkins at http://localhost:8080/

Install recommended plugins during setup.

Install Git and Docker Pipeline plugins if missing.

Create a New Pipeline Job named task2-devops-internship.

Connect your GitHub repository under:

Pipeline → Definition → Pipeline script from SCM
SCM: Git
Repository URL: https://github.com/girishpatil2102/task-2-devops-internship.git
Branch: main

3️⃣ Create Jenkinsfile in GitHub Repo
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Building Docker image...'
                bat '''
                    set DOCKER_BUILDKIT=0
                    docker build -t task2-devops-internship .
                '''
            }
        }
    }
}

4️⃣ Start Jenkins Server

Start Jenkins from the command line:

java -jar jenkins.war


or via Windows service at http://localhost:8080.

5️⃣ Run Ngrok Tunnel

Expose Jenkins to the internet (for GitHub webhook):

ngrok http 8080


Example output:

Forwarding  https://rosann-leisureless-suppositionally.ngrok-free.dev -> http://localhost:8080

6️⃣ Configure GitHub Webhook

Go to your GitHub repo → Settings → Webhooks → Add Webhook

Set:

Payload URL: https://<ngrok_url>/github-webhook/

Content type: application/json

Trigger: Just the push event

Save webhook and ensure the status shows “✅ Delivered successfully”

7️⃣ Test the CI/CD Pipeline

Make a small change in your code (e.g., update app.js or README).

Commit and push to GitHub.

Jenkins automatically triggers the pipeline.

Check Jenkins stages:

✅ Checkout successful

✅ Dependencies installed

✅ Tests executed

✅ Docker image built successfully

🐳 Dockerfile Used
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]

🧰 Common Errors & Fixes

❌ Webhook “Failed to connect to host”	:- Jenkins not publicly accessible	:- Start ngrok http 8080 and use the ngrok URL

❌ “Docker daemon not running”	:- Docker service stopped 	:- 	Start Docker Desktop

❌ “Parent snapshot not found” 	:- 	Docker BuildKit cache issue		:-  Run docker system prune -a --volumes -f and retry

❌ Slow build	 	:-  Large image download		:-  Pre-pull image docker pull node:18


📊 Final Output Example

Stage: Checkout   → SUCCESS

Stage: Build      → SUCCESS

Stage: Test       → SUCCESS

Stage: Deploy     → SUCCESS

Docker image built: task2-devops-internship:latest


Jenkins logs confirm:

Started by GitHub push by girishpatil2102
Finished: SUCCESS

🏁 Outcome


Implemented a fully automated CI/CD pipeline using Jenkins, Docker, and GitHub Webhooks.

Configured ngrok for webhook tunneling from local Jenkins.

Automated build, test, and Docker image creation upon every code push.

Screenshots :-


<img width="1920" height="1080" alt="Screenshot 2025-10-22 190410" src="https://github.com/user-attachments/assets/cbc4fcd8-6c6d-4443-9835-bf10c93d8b28" />

<img width="1920" height="1080" alt="Screenshot 2025-10-22 190607" src="https://github.com/user-attachments/assets/54d3cc13-8e94-456a-824e-f66cbef38a22" />


<img width="1920" height="1080" alt="Screenshot 2025-10-22 193240" src="https://github.com/user-attachments/assets/d46e4edb-7e58-4f23-ad2b-0b88d2cbbbb2" />


<img width="1920" height="1080" alt="Screenshot 2025-10-22 212934" src="https://github.com/user-attachments/assets/7577b3b3-5a0f-497a-80f8-b6b045b51838" />


👨‍🎓 Author

Girish Patil
DevOps Internship Project — Task 2: CI/CD Pipeline Implementation
GitHub: girishpatil2102
