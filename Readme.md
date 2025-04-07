# Node.js CI/CD Demo with Docker and GitHub Actions

This repository demonstrates setting up an automated CI/CD pipeline using GitHub Actions for a simple Node.js Express application. The pipeline builds a Docker image of the application and pushes it to Docker Hub upon every push to the `master` branch.

This project is based on the original [heroku/node-js-sample](https://github.com/heroku/node-js-sample) application.

---

### Original Repository Note:

**The original `heroku/node-js-sample` repository is no longer maintained!**

**For the most up to date test app to get you started on Heroku, head on over to [`node-js-getting-started`](https://github.com/heroku/node-js-getting-started).**

---

## Features

*   A barebones Node.js app using [Express 4](http://expressjs.com/).
*   **Dockerized:** Includes a `Dockerfile` for building a container image.
*   **CI/CD Pipeline:** Uses GitHub Actions (`.github/workflows/main.yml`) to:
    *   Checkout code.
    *   Set up Node.js environment.
    *   Install dependencies (`npm install`).
    *   Run tests (`npm test`) - *Note: Currently, no test script is defined in `package.json`, so this step might fail or do nothing.*
    *   Build a Docker image.
    *   Log in to Docker Hub (requires secrets).
    *   Push the Docker image to Docker Hub.

## Prerequisites

*   [Node.js](http://nodejs.org/) (v14 or compatible, as used in Dockerfile and Workflow)
*   [npm](https://www.npmjs.com/) (comes with Node.js)
*   [Git](https://git-scm.com/)
*   [Docker](https://www.docker.com/) (for building and running the container locally)

## Running Locally (Standard Node)

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/dasaradhi10/dasaradhi10-automate-code-deployment-using-ci-cd-pipeline-github-actions.git
    cd dasaradhi10-automate-code-deployment-using-ci-cd-pipeline-github-actions
    ```

2.  **Install dependencies:**
    ```sh
    npm install
    ```

3.  **Start the application:**
    ```sh
    npm start
    ```

Your app should now be running on [localhost:5000](http://localhost:5000/). The port is determined by the `PORT` environment variable or defaults to 5000 (`index.js`).

## Running Locally (Using Docker)

1.  **Build the Docker image:**
    ```sh
    # Replace 'your-dockerhub-username' if desired, or use a local tag
    docker build -t node-js-sample-app .
    ```
    *Note: The CI/CD pipeline tags the image as `<your-dockerhub-username>/node-js-sample`.*

2.  **Run the Docker container:**
    ```sh
    # This runs the container in detached mode and maps port 5000 on your host
    # to port 5000 inside the container (where the Node app listens by default)
    docker run -p 5000:5000 -d node-js-sample-app
    ```
    *   `-p 5000:5000`: Maps port 5000 on your host machine to port 5000 inside the container.
    *   `-d`: Runs the container in the background (detached mode).
    *   `node-js-sample-app`: The name we tagged the image with in the build step.

Your app should now be running in a Docker container, accessible via [localhost:5000](http://localhost:5000/).

*Note: The `Dockerfile` includes `EXPOSE 3000`, which is informational. The application itself (`index.js`) listens on `process.env.PORT || 5000`. The `docker run` command above maps the host port to the application's default port (5000).*

## CI/CD Pipeline (GitHub Actions)

The workflow defined in `.github/workflows/main.yml` automates the build and deployment process.

**Trigger:**
*   Runs automatically on every `push` to the `master` branch.

**Jobs:**
*   `build-and-deploy`: Runs on an `ubuntu-latest` runner.

**Steps:**
1.  **Checkout Code:** Checks out the repository code.
2.  **Set up Node.js:** Configures the runner with Node.js version 14.
3.  **Install Dependencies:** Runs `npm install` to fetch project dependencies.
4.  **Run Tests:** Executes `npm test`. **(Note: No `test` script is defined in `package.json`. Add tests and a corresponding script for this step to be meaningful).**
5.  **Build Docker Image:** Builds the Docker image using the `Dockerfile` and tags it as `<DOCKER_USERNAME>/node-js-sample`.
6.  **Log in to DockerHub:** Authenticates with Docker Hub using secrets.
7.  **Push Docker Image:** Pushes the built image to Docker Hub.

**Required Secrets:**
For the pipeline to successfully push to Docker Hub, you need to configure the following secrets in your GitHub repository settings (`Settings` > `Secrets and variables` > `Actions`):
*   `DOCKER_USERNAME`: Your Docker Hub username.
*   `DOCKER_PASSWORD`: Your Docker Hub password or preferably an [Access Token](https://docs.docker.com/docker-hub/access-tokens/).

## Configuration

*   **PORT:** The application listens on the port specified by the `PORT` environment variable. If not set, it defaults to `5000`. This is standard practice for platforms like Heroku and can be set when running Docker containers (`docker run -e PORT=8080 ...`).

