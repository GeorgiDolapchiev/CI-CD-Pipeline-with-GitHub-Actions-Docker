CI/CD Pipeline with GitHub Actions + Docker

This project showcases a streamlined Continuous Integration and Continuous Deployment (CI/CD) pipeline built with GitHub Actions and Docker. It automates the process of building, testing, and deploying a containerized application, demonstrating modern DevOps practices for efficient and reliable software delivery.

Features





Automated Builds: Triggers Docker image builds on code pushes or pull requests to the main branch.



Testing: Runs automated tests (e.g., unit tests or linting) to ensure code quality.



Docker Integration: Builds and pushes Docker images to a container registry (e.g., Docker Hub or GitHub Container Registry).



Extensible Deployment: Configurable for deploying to staging or production environments.



Email Notifications: Includes testing for pipeline status notifications via email.

Technologies Used





GitHub Actions: Workflow automation for CI/CD processes.



Docker: Containerization for consistent development and production environments.



YAML: Configuration for defining pipeline workflows.

Prerequisites

To run this project locally or extend it, ensure you have:





A GitHub account with a repository.



Docker installed for building and testing containers.



A Docker Hub or GitHub Container Registry account (optional for pushing images).



Basic understanding of YAML and Docker for configuration.

Setup Instructions





Clone the Repository:

git clone https://github.com/GeorgiDolapchiev/CI-CD-Pipeline-with-GitHub-Actions-Docker.git
cd CI-CD-Pipeline-with-GitHub-Actions-Docker



Create a Dockerfile:





Add a Dockerfile in the project root to define your application’s build process. Example for a Node.js app:

FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]



Configure GitHub Secrets:





Navigate to your GitHub repository: Settings > Secrets and variables > Actions.



Add secrets for registry authentication (e.g., DOCKER_USERNAME and DOCKER_PASSWORD for Docker Hub).



Test Locally:





Build the Docker image:

docker build -t my-app .



Run the container:

docker run -p 3000:3000 my-app

CI/CD Pipeline

The pipeline is defined in .github/workflows/ci-cd.yml and runs on pushes to the main branch or pull requests.

Workflow Steps





Checkout Code: Retrieves the latest repository code.



Set Up Environment: Installs required dependencies (e.g., Node.js, Python).



Run Tests: Executes automated tests to validate code.



Build Docker Image: Creates a Docker image using the Dockerfile.



Push to Registry: Pushes the image to a container registry.



Send Notifications: Tests email notifications for pipeline status (success/failure).

Example Workflow (ci-cd.yml)

name: CI/CD Pipeline
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Build and push Docker image
        run: |
          docker build -t ${{ secrets.DOCKER_USERNAME }}/my-app:latest .
          docker push ${{ secrets.DOCKER_USERNAME }}/my-app:latest

Monitor pipeline runs in the Actions tab of your GitHub repository.

Usage





Push changes to the main branch or create a pull request to trigger the pipeline.



Check the Actions tab for build logs and pipeline status.



Extend the pipeline for deployment (e.g., to AWS, Kubernetes, or a VPS) by adding deployment steps.

Project Structure

├── .github/workflows/ci-cd.yml  # GitHub Actions workflow file
├── Dockerfile                  # Docker configuration for the app
├── README.md                   # Project documentation
└── src/                        # Application source code (e.g., Node.js app)

Contributing

Contributions are welcome! To contribute:





Fork the repository.



Create a new branch (git checkout -b feature-branch).



Commit your changes (git commit -m "Add feature").



Push to the branch (git push origin feature-branch).



Open a pull request with a detailed description.

License

This project is licensed under the MIT License.

Contact

For questions or suggestions, reach out to Georgi Dolapchiev via GitHub.



This project is a portfolio piece demonstrating my ability to implement CI/CD pipelines using GitHub Actions and Docker, streamlining development workflows and ensuring reliable deployments.
