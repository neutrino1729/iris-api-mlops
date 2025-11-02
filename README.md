# Iris API - MLOps with CI/CD

This project demonstrates Continuous Integration and Continuous Deployment (CI/CD) for an Iris classification API using FastAPI, Docker, and Kubernetes on GCP.

## Architecture

- **API Framework**: FastAPI
- **Containerization**: Docker
- **Container Registry**: Google Artifact Registry
- **Orchestration**: Google Kubernetes Engine (GKE)
- **CI/CD**: GitHub Actions

## Kubernetes vs Docker

### Docker Container
- A Docker container is a **lightweight, standalone, executable package** that includes everything needed to run a piece of software (code, runtime, libraries, dependencies).
- Containers run in isolation on a single host machine.
- Managed individually using Docker commands.

### Kubernetes Pod
- A Kubernetes Pod is the **smallest deployable unit** in Kubernetes.
- A Pod can contain **one or more containers** that share storage, network, and specifications.
- Pods are managed by Kubernetes, which provides orchestration, scaling, self-healing, and load balancing.
- Pods are ephemeral and can be created/destroyed by Kubernetes automatically.

**Key Difference**: Docker containers are the actual runtime instances, while Kubernetes Pods are an abstraction layer that manages one or more containers with shared resources.

## API Endpoints

- `GET /` - Welcome message
- `POST /predict/` - Predict iris species

## Local Testing
```bash
# Build Docker image
docker build -t iris-api .

# Run container
docker run -d -p 8200:8200 iris-api

# Test API
curl -X POST "http://localhost:8200/predict/" \
  -H "Content-Type: application/json" \
  -d '{"sepal_length": 5.1, "sepal_width": 3.5, "petal_length": 1.4, "petal_width": 0.2}'
```

## Deployment

Deployment happens automatically via GitHub Actions when code is pushed to the `main` branch.

## Project Structure
```
iris-api-mlops/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions CI/CD pipeline
├── iris_fastapi.py              # FastAPI application
├── model.joblib                 # Trained ML model
├── requirements.txt             # Python dependencies
├── Dockerfile                   # Docker image definition
├── k8s-namespace.yaml           # Kubernetes namespace
├── k8s-deployment.yaml          # Kubernetes deployment config
├── k8s-service.yaml             # Kubernetes service (LoadBalancer)
└── README.md                    # This file
```
