Steps to achieve this Tasks🚀
Project: Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)

For today's project, "Automate Code Deployment Using CI/CD Pipeline (GitHub Actions)," here's a brief step-by-step process and results:

### Step-by-Step Process:
1. **Setup GitHub Repository:**
   - Forked the 'node-js-sample' repository on GitHub.
   - Cloned the repository to your local machine using Git.

2. **Install Required Tools:**
   - Installed Git, Docker, and Node.js on your machine.
   - Logged into Docker Desktop using your DockerHub account.

3. **Create and Configure GitHub Actions Workflow:**
   - Created a `.yml` file in the `.github/workflows` directory of the repo.
   - Defined the CI/CD pipeline process in the file, including the necessary steps for building and testing the Node.js application using GitHub Actions.

4. **Set Up Docker:**
   - Built and tested the Docker image of the application to ensure it was working correctly.

5. **Run the CI/CD Pipeline:**
   - Pushed changes to the GitHub repository, triggering the GitHub Actions workflow.
   - The pipeline automatically built and tested the Node.js application, then pushed the Docker image to DockerHub.

### Results:
- Successfully automated the code deployment using GitHub Actions.
- Docker images were successfully created and uploaded to DockerHub.
- The Node.js application was deployed seamlessly using the CI/CD pipeline.

This project streamlined the process of deploying code, ensuring quick updates and reliability in the development cycle.

🛠 Step 1: Environment Setup
Installed Git for version control.
Installed Docker and logged in using DockerHub credentials.
Installed Node.js and npm for running and managing the Node.js app.

🔀 Step 2: Project Setup
Forked the repository node-js-sample from GitHub.
Cloned it to local using:

bash
Copy
Edit
git clone https://github.com/dasaradhi10/node-js-sample.git
Navigated into the repo and ensured everything was working by running:

bash
Copy
Edit
npm install
npm test

🐳 Step 3: Docker Configuration
Created a Dockerfile to containerize the Node.js app.

Verified the Docker image by building and running it locally:
docker build -t dasaradhi10/node-js-sample .
docker run -p 3000:3000 dasaradhi10/node-js-sample

Step 4: GitHub Secrets
Created DockerHub access secrets in GitHub repo:
DOCKER_USERNAME - *********

DOCKER_PASSWORD - **********

⚙️ Step 5: CI/CD Workflow Configuration
Created .github/workflows/main.yml file with the following actions:

Checkout code

Set up Node.js

Install dependencies

Run tests

Build Docker image

Login to DockerHub

Push image to DockerHub

✅ Step 6: Triggering CI/CD Pipeline
Pushed changes to master branch.
GitHub Actions pipeline triggered automatically.
Faced and resolved several issues like:
Invalid Docker tags
Docker login failures
Syntax errors in .yml
Push denied errors
📤 Step 7: Uploading to GitHub
Created a new repo for this task.

Uploaded:
Code (Dockerfile, .yml, source code)
README.md
Screenshots (pipeline result)
