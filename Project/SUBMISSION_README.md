## Multi-Container Docker Application with CI/CD: Calculator App Project

#### Complete Project Instructions: [DevOps Foundations Course/Project](https://github.com/shiftkey-labs/DevOps-Foundations-Course/tree/master/Project)

#### Submission by - **Ethan Hankinson**

### Project Overview

- **Brief project description:** What is the purpose of your application?

    The purpose of this project is to build a calculator web application that features both a backend API (written in Python) and a frontend React application. These components will be containerized using Docker, orchestrated with Docker Compose, and automatically deployed using a CI/CD pipeline.


- **Which files are you implmenting? and why?:**
    - `Dockerfile` for the backend (Python API) to containerize the backend service.
    - `Dockerfile` for the frontend (React app) to containerize the frontend service.
    - `docker-compose.yml` to orchestrate the services and enable communication between the frontend and backend containers.
    - CI/CD pipeline YAML configuration to automate the build, test, and deployment processes.


- _**Any other explanations for personal note taking.**_
    - Ensure Docker images are optimized for production by reducing the number of layers in Dockerfiles.
    - Use environment variables for configuration settings that differ between environments (e.g., dev, production).


### Docker Implementation

**Explain your Dockerfiles:**

- **Backend Dockerfile** (Python API):
    
The Dockerfile for the backend API is built on a Python base image. It sets up the environment for running a Flask API, installs the necessary Python dependencies from a requirements.txt file, and exposes the port 5000 for communication.

Key Steps:

    1. Start from a Python 3.9 base image.
    2. Set the working directory and copy the project files into the container.
    3. Install dependencies using pip.
    4. Expose the required port for the application (5000).
    5. Set the command to run the Flask app.

- **Frontend Dockerfile** (React App):
    
This Dockerfile is based on the official Node.js image. It builds the React app and serves it using a lightweight web server (Nginx) to serve the static files.

Key Steps:

    1. Use the Node.js image for building the app.
    2. Copy the React app's source code and install dependencies using npm install.
    3. Build the React app for production.
    4. Serve the built app using Nginx.

**Use this section to document your choices and steps for building the Docker images.**

- Backend image uses Python and Flask for simplicity and flexibility.
- Frontend image uses Node.js for building the React app and Nginx for serving static files in production.

### Docker Compose YAML Configuration

**Break down your `docker-compose.yml` file:**

- **Services:** List the services defined. What do they represent?

    - frontend: Represents the React frontend application.
    - backend: Represents the Python API that the frontend interacts with.
- **Networking:** How do the services communicate with each other?

    - Both services are in the same Docker network, allowing them to communicate using service names (e.g., `frontend` can call `backend:5000`).
- **Volumes:** Did you use any volume mounts for persistent data?

    No persistent data is needed for this project, so volumes aren’t used.
- **Environment Variables:** Did you define any environment variables for configuration? 

    - The backend service uses an environment variable for the API's configuration (e.g., `FLASK_ENV` for development or production).

**Use this section to explain how your services interact and are configured within `docker-compose.yml`.**

    - The frontend service makes API calls to the backend via the backend service name defined in the docker-compose.yml.
    - The backend is exposed on port 5000.
    - The frontend is exposed on port 80 for easy access.


### CI/CD Pipeline (YAML Configuration)

**Explain your CI/CD pipeline:**

- What triggers the pipeline (e.g., push to main branch)? 

The pipeline is triggered on every push to the main branch.
- What are the different stages (build, test, deploy)?
- Build: Builds Docker images for both frontend and backend.
- Test: Runs tests for the frontend and backend code.
- Deploy: Deploys the Docker containers to the appropriate environment (staging/production).

- How are Docker images built and pushed to a registry (if applicable)?
The Docker images are built in the pipeline and pushed to a Docker registry (e.g., Docker Hub or AWS ECR). This ensures that the latest version of the app is always available for deployment.

**Use this section to document your automated build and deployment process.**

- The frontend service makes API calls to the backend via the backend service name defined in the docker-compose.yml.
- The backend is exposed on port 5000.
- The frontend is exposed on port 80 for easy access.


### CI/CD Pipeline (YAML Configuration)

**Simply explain your CI/CD pipeline:**

Trigger: The pipeline is triggered on every push to the main branch.

Stages:

- Build: Builds Docker images for both frontend and backend.
- Test: Runs tests for the frontend and backend code.
- Deploy: Deploys the Docker containers to the appropriate environment (staging/production).

Docker images build and push:
    
The Docker images are built in the pipeline and pushed to a Docker registry (e.g., Docker Hub or AWS ECR). This ensures that the latest version of the app is always available for deployment.

**Use this section to document your automated build, and docker process.**

- Docker images are tagged with the commit SHA for traceability.
- The pipeline ensures that the images are tested before deployment.


### Assumptions

- The backend API has no database or persistent storage, so no database configuration is necessary.
- The frontend and backend are designed to be stateless and can be redeployed without data loss.
- The CI/CD pipeline is set up to deploy to a cloud provider that supports Docker containers (e.g., AWS ECS or Azure App Services).


### Lessons Learned

- What challenges did you encounter while working with Docker and CI/CD?
- What did you learn about containerization and automation?

**Use this section to reflect on your experience and learnings when implementing this project.**

Challenges:

- Ensuring that the frontend and backend services could communicate over the Docker network.
- Dealing with the complexity of setting up a CI/CD pipeline that automates Docker image building and deployment.
Learnings:

- Dockerization provides an easy way to ensure the same environment across development, staging, and production.
- CI/CD pipelines significantly streamline the process of deploying new features and bug fixes.


### Future Improvements

Dockerfiles:

- Improve the security of the images by reducing unnecessary layers and ensuring that sensitive information is not hardcoded.
CI/CD Pipeline:

- Implement automated rollback strategies in case of failed deployments.
- Add stages to deploy to different environments (e.g., dev, staging) based on the branch pushed to.

Additional Features for the Calculator App:

- Implement additional features like unit conversions or more complex mathematical operations to further improve the app’s functionality.

