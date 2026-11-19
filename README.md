# Automated CI/CD Pipeline for a Flask Application

## Project Overview

This project demonstrates the implementation of an automated Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Python Flask application using GitHub Actions, Docker, and Docker Hub.

The pipeline automatically runs application tests whenever code is pushed to the `main` branch or a pull request is opened against it. On successful pushes to `main`, the application is packaged into a Docker image and published to Docker Hub.

The project is being developed further to include deployment on Amazon Web Services (AWS).

## Technologies Used

- **Python 3.11** – Application programming language.
- **Flask** – Python web framework.
- **Pytest** – Automated application testing.
- **Docker** – Application containerization.
- **GitHub** – Source code management.
- **GitHub Actions** – CI/CD automation.
- **Docker Hub** – Container image registry.
- **AWS** – Planned cloud deployment platform.

## Project Structure

```text
automated-cicd-pipeline/
│
├── .github/
│   └── workflows/
│       └── ci-cd.yml
│
├── app/
│
├── tests/
│
├── .dockerignore
├── .gitignore
├── Dockerfile
├── requirements.txt
└── README.md
```

## Application Endpoints

The Flask application currently exposes the following endpoints:

| Endpoint | Description |
|---|---|
| `/` | Returns the application welcome message and running status. |
| `/health` | Returns the application health status. |

Example homepage response:

```json
{
  "application": "Automated CI/CD Pipeline",
  "message": "Hello from AWS!",
  "status": "running"
}
```

Example health response:

```json
{
  "status": "healthy"
}
```

## Running the Application with Docker

### 1. Clone the repository

```bash
git clone https://github.com/IphyDigiTech/automated-cicd-pipeline.git

cd automated-cicd-pipeline
```

### 2. Build the Docker image

```bash
docker build -t flask-cicd-app:local .
```

### 3. Run the Docker container

```bash
docker run -d \
  --name flask-cicd-container \
  -p 5000:5000 \
  flask-cicd-app:local
```

### 4. Access the application

Open your browser:

- Homepage: http://localhost:5000
- Health check: http://localhost:5000/health

Alternatively, test using curl:

```bash
curl http://localhost:5000
curl http://localhost:5000/health
```

## Running Automated Tests

The project uses Pytest for automated testing.

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Run the tests:

```bash
python -m pytest -v
```

The current test suite verifies the homepage and health-check endpoints.

## CI/CD Pipeline

GitHub Actions automates the Continuous Integration and Docker image publishing process.

The workflow is located at:

```text
.github/workflows/ci-cd.yml
```

### Pipeline workflow

1. Developer pushes code to the GitHub repository.
2. GitHub Actions checks out the repository.
3. Python dependencies are installed.
4. Automated Flask tests are executed.
5. If tests pass on a push to `main`, Docker Buildx builds the application image.
6. GitHub Actions authenticates with Docker Hub.
7. The Docker image is published to Docker Hub.

### Pipeline triggers

- Pushes to the `main` branch.
- Pull requests targeting the `main` branch.

The Docker publishing job runs only after successful tests on pushes to `main`.

## Docker Hub Repository

The application image is published to:

https://hub.docker.com/r/iphydigitech/flask-cicd-app

Available image tags:

- `latest`
- Git commit SHA

To pull the published image:

```bash
docker pull iphydigitech/flask-cicd-app:latest
```

To run it:

```bash
docker run -d \
  --name flask-cicd-container \
  -p 5000:5000 \
  iphydigitech/flask-cicd-app:latest
```

## Security Practices

- GitHub Actions secrets are used to store Docker Hub credentials.
- Access tokens are used instead of account passwords for Docker Hub authentication.
- Credentials and sensitive information should never be committed to the GitHub repository.
- AWS deployment credentials and permissions will be configured securely during the cloud deployment stage.

## AWS Deployment (Planned)

The next development phase will extend the pipeline to AWS.

Planned AWS services and capabilities include:

- Amazon EC2 for hosting the Flask application.
- Amazon ECR for storing Docker images.
- AWS IAM for access management.
- AWS Systems Manager for deployment management.
- GitHub Actions with OpenID Connect (OIDC) for secure AWS authentication.
- Automated deployment of updated application images.

**Note:** AWS resources and deployment automation have not yet been configured for this project.

## Project Status

- [x] Flask application created.
- [x] Application endpoints implemented.
- [x] Automated tests created.
- [x] Dockerfile configured.
- [x] Docker image built and tested locally.
- [x] GitHub repository created.
- [x] GitHub Actions CI workflow configured.
- [x] Automated Docker image publishing configured.
- [x] Docker image successfully published to Docker Hub.
- [x] Published Docker image pulled and tested locally.
- [ ] AWS infrastructure setup.
- [ ] AWS deployment automation.
- [ ] Public application deployment.

 Author

**IphyDigiTech**

GitHub: https://github.com/IphyDigiTech

Project Repository: https://github.com/IphyDigiTech/automated-cicd-pipeline
