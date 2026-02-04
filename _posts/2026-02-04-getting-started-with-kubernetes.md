---
layout: post
title: "Getting Started with Kubernetes"
date: 2026-02-04 11:00:00 +0800
categories: [kubernetes, tutorial]
tags: [kubernetes, k8s, containers, devops]
---

Kubernetes has become the de facto standard for container orchestration. In this post, I'll share some fundamentals to help you get started.

## What is Kubernetes?

Kubernetes (K8s) is an open-source container orchestration platform that automates:

- Deployment of containerized applications
- Scaling based on demand
- Management of container lifecycles
- Load balancing and service discovery

## Key Concepts

### Pods

The smallest deployable unit in Kubernetes. A pod can contain one or more containers.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: app
    image: nginx:latest
    ports:
    - containerPort: 80
```

### Deployments

Manage the desired state of your application:

```yaml
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
      - name: app
        image: nginx:latest
```

### Services

Expose your applications:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
  - port: 80
    targetPort: 80
  type: ClusterIP
```

## Learn More

Check out my [K8sLabs repository](https://github.com/ChunPingWang/K8sLabs) for hands-on exercises.

Happy learning!
