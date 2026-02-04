# Containerized Web Application Deployment using Docker & Kubernetes

A simple static web application containerized with Docker and deployed on Kubernetes using Minikube. This project demonstrates the fundamentals of container orchestration and the deployment lifecycle.

---

## Tech Stack

- **Frontend**: HTML, CSS, JavaScript
- **Web Server**: Nginx
- **Containerization**: Docker
- **Orchestration**: Kubernetes (Minikube)
- **Tools**: kubectl

---

## Architecture

```
┌─────────────────┐
│   Browser       │
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│  Kubernetes Service     │
│  (NodePort)             │
│  Routes external traffic│
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Kubernetes Deployment  │
│  Manages Pod lifecycle  │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Pod                    │
│  ┌───────────────────┐  │
│  │ Nginx Container   │  │
│  │ (nginx:alpine)    │  │
│  └───────────────────┘  │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Static Files           │
│  HTML / CSS / JS        │
└─────────────────────────┘
```

**Flow**:
1. Browser sends HTTP request to NodePort Service
2. Service routes traffic to Pod using label selectors
3. Pod runs Nginx container serving static files
4. Nginx returns the web application to the browser

---

## Project Structure

```
.
├── Dockerfile
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
└── website/
    ├── index.html
    ├── cheet.css
    ├── cheet.js
    └── commands.js
```

---

## Docker Implementation

The Dockerfile uses `nginx:alpine` as the base image and copies static files into the Nginx web root.

**Key steps**:
- Remove default Nginx content
- Copy custom HTML/CSS/JS files
- Expose port 80

---

## Kubernetes Implementation

**Deployment**: Manages the Pod lifecycle and ensures the application stays running.

**Service (NodePort)**: Exposes the application externally and routes traffic using labels.

---

## How to Run

1. **Build the Docker image**
   ```bash
   docker build -t cheatsheet-app .
   ```

2. **Load image into Minikube**
   ```bash
   minikube image load cheatsheet-app
   ```

3. **Apply Kubernetes resources**
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

4. **Access the application**
   ```bash
   minikube service cheatsheet-service
   ```

5. **Verify deployment**
   ```bash
   kubectl get pods
   kubectl get services
   ```

---

## Debugging Commands

```bash
# Check Pod status
kubectl get pods

# View Pod details
kubectl describe pod <pod-name>

# Check logs
kubectl logs <pod-name>

# Verify Service
kubectl get svc
kubectl describe svc <service-name>
```

---

## Learning Outcomes

- Containerized a static application using Docker
- Deployed and managed containers using Kubernetes
- Understood the role of Deployments and Services
- Gained hands-on experience with Minikube and kubectl
- Developed debugging skills for containerized applications

---

## Future Enhancements

- Add replicas for high availability
- Implement health checks (liveness/readiness probes)
- Set up Ingress for better routing
- Deploy to a cloud Kubernetes service (EKS, GKE, AKS)
- Add CI/CD pipeline for automated deployments

---

## Author

Built as a learning project to demonstrate Docker and Kubernetes fundamentals.