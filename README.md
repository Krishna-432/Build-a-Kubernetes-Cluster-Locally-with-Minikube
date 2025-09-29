# Build-a-Kubernetes-Cluster-Locally-with-Minikube

# 🚀 Build a Kubernetes Cluster Locally with Minikube

This demonstrates how to deploy and manage applications in Kubernetes using **Minikube**, **kubectl**, and **Docker**.

---

## 📂 Directory Structure

```

k8s-minikube-task/
│── deployment.yaml
│── service.yaml
│── README.md

````

---

## ⚡ Step-by-Step Guide

### Step 1: Install & Start Minikube

#### On Linux/macOS
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
````

#### On Windows (PowerShell as Admin)

```powershell
choco install minikube -y
```

#### Start Cluster

```bash
minikube start --driver=docker
```

✅ **What we achieved:** A local Kubernetes cluster running inside Docker.




---

### Step 2: Verify Cluster

```bash
kubectl get nodes
```

✅ **What we achieved:** Node(s) are ready.







---

### Step 3: Create a Deployment

**deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deployment
  labels:
    app: hello-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hello-app
  template:
    metadata:
      labels:
        app: hello-app
    spec:
      containers:
      - name: hello-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

Apply:

```bash
kubectl apply -f deployment.yaml
```

✅ **What we achieved:** 2 pods running NGINX.





---

### Step 4: Expose Deployment via Service

**service.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-service
spec:
  selector:
    app: hello-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort
```

Apply:

```bash
kubectl apply -f service.yaml
```

✅ **What we achieved:** Pods exposed via NodePort service.




---

### Step 5: Access the App

```bash
minikube service hello-service
```

✅ **What we achieved:** Opened NGINX welcome page in browser.






---

### Step 6: Scaling Deployment

```bash
kubectl scale deployment hello-deployment --replicas=4
kubectl get pods
```

✅ **What we achieved:** Deployment scaled to 4 pods.






---

### Step 7: Describe & Logs

```bash
kubectl describe deployment hello-deployment
kubectl logs <pod-name>
```

✅ **What we achieved:** Checked pod details & logs.






---



