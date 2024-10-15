# Kubernetes Image Deployment in Pods, ReplicaSets & Deployments

This project demonstrates how to deploy Docker images using Kubernetes in Pods, ReplicaSets, and Deployments. It provides examples for setting up and managing different Kubernetes objects to deploy containerized applications.

## Prerequisites

- **Docker**: To build and containerize your application.
- **Kubernetes (kubectl)**: For managing Kubernetes resources.
- **Minikube** (optional): For running a local Kubernetes cluster.

## Getting Started

### Step 1: Build and Push Docker Image

Ensure you have Docker installed, and then build your image:

```bash
docker build -t <your_image_name> .
docker push <your_image_name>

### Step 2: Deploy to Kubernetes
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: <your_image_name>
      ports:
        - containerPort: 80
**Deploy the Pod:**
  kubectl apply -f pod.yaml
**ReplicaSet**
To create a ReplicaSet that ensures a specific number of Pods are running:
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: <your_image_name>
          ports:
            - containerPort: 80
**Deploy the ReplicaSet:**
   kubectl apply -f replicaset.yaml
**Deployment**
   A Deployment provides declarative updates to Pods and ReplicaSets:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-container
          image: <your_image_name>
          ports:
            - containerPort: 80
**Deploy the Deployment:**
  kubectl apply -f deployment.yaml

###Step 3: Scale and Manage Resources
To scale the number of replicas in a ReplicaSet or Deployment:
  kubectl scale --replicas=5 deployment/my-deployment
###Step 4: Cleanup
To delete all resources:
kubectl delete deployment my-deployment
kubectl delete replicaset my-replicaset
kubectl delete pod my-pod
