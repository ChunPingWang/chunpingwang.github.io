---
layout: post
title: "Kubernetes Hands-On Labs: From Zero to Production"
date: 2026-02-04 15:00:00 +0800
categories: [kubernetes, tutorial]
tags: [kubernetes, k8s, kind, containers, devops, labs]
---

Learning Kubernetes requires hands-on practice. I've created K8sLabs, a comprehensive workshop for mastering Kubernetes fundamentals through practical exercises.

## Why Kubernetes?

Kubernetes evolved from Google's internal system called Borg, which has been managing containers at massive scale for over a decade. Today, K8s is the industry standard for:

- Container orchestration
- Self-healing deployments
- Horizontal scaling
- Service discovery
- Configuration management

## Setting Up a Local Cluster with Kind

Kind (Kubernetes in Docker) is perfect for learning:

```bash
# Install kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# Create a multi-node cluster
cat <<EOF | kind create cluster --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
EOF
```

## Core Concepts Covered

### 1. Namespaces

Organize and isolate resources:

```bash
kubectl create namespace dev
kubectl create namespace prod
kubectl get namespaces
```

### 2. Pods

The smallest deployable unit:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

### 3. Multi-Container Pods

Containers in the same pod share network and storage:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-container
spec:
  containers:
  - name: app
    image: my-app:latest
  - name: sidecar
    image: log-collector:latest
```

### 4. Deployments

Manage replicas and updates:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:latest
```

### 5. Jobs and CronJobs

Batch processing:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: backup-job
spec:
  schedule: "0 2 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: backup
            image: backup-tool:latest
          restartPolicy: OnFailure
```

### 6. Services

Network abstraction for pods:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web
  ports:
  - port: 80
    targetPort: 80
  type: ClusterIP
```

## Workshop Structure

The labs progress from basics to advanced topics:

1. Environment setup with Vagrant/Kind
2. Namespace and resource organization
3. Pod lifecycle management
4. Deployment strategies
5. Service networking
6. ConfigMaps and Secrets
7. Persistent storage

## Get Started

Clone the repository and follow along: [K8sLabs](https://github.com/ChunPingWang/K8sLabs)

The best way to learn Kubernetes is by doing. Start with the labs and build your confidence!
