# Examination-assignment


This repository contains a simple Nginx-based web application containerized with Docker and deployed using Kubernetes. The Docker images are publicly available and can be pulled from GitHub Container Registry (GHCR).

## Prerequisites

Ensure you have the following installed on your system:
- **Docker** (for running containers)
- **Kubernetes (kubectl & minikube/kind or a cluster)** (for deployment)
- **Ansible** (for automation)

## Clone the Repository

```sh
git clone git@github.com:salah-96/Examination-assignment.git
cd Examination-assignment
```

## Pull and Run the Docker Image

You can pull and run the latest available Docker image:

### Version 1.0.0
```sh
docker pull ghcr.io/salah-96/examination-assignment:v1.0.0
docker run -p 8080:80 ghcr.io/salah-96/examination-assignment:v1.0.0
```

### Version 1.1.0
```sh
docker pull ghcr.io/salah-96/examination-assignment:v1.1.0
docker run -p 8080:80 ghcr.io/salah-96/examination-assignment:v1.1.0
```

Once the container is running, open [http://localhost:8080](http://localhost:8080) in your browser.

## Deploying to Kubernetes

### Apply the Deployment
```sh
kubectl apply -f nginx-deployment.yaml
```

### Verify Deployment
```sh
kubectl get pods
kubectl get services
```

### Access the Application
If using **minikube**, you may need to expose the service:
```sh
minikube service nginx-service
```
Otherwise, check the NodePort and access it via `http://<your-cluster-ip>:<NodePort>`.

## Automating with Ansible
This repository also contains an Ansible playbook (`ansible-playbook.yaml`) for automation.
Run the playbook:
```sh
ansible-playbook ansible-playbook.yaml
```

## CI/CD Pipeline
This project uses **GitHub Actions** to:
- Build and push the Docker image to GHCR.
- Trigger the pipeline on **annotated Git tags**.
- Ensure no cached layers are used during build.

To trigger the pipeline, create and push an annotated tag:
```sh
git tag v1.2.0 -m "New version"
git push origin v1.2.0
```
