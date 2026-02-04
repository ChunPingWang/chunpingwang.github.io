---
layout: post
title: "Installing Tanzu Application Platform on Minikube"
date: 2026-02-04 13:00:00 +0800
categories: [devops, kubernetes]
tags: [tanzu, tap, vmware, kubernetes, minikube, platform-engineering]
---

Tanzu Application Platform (TAP) is VMware's developer platform built on Kubernetes. It provides a complete toolchain for building and deploying applications. Here's how to set it up on a local minikube cluster.

## Prerequisites

- Ubuntu Desktop (or similar Linux)
- Minikube installed
- At least 16GB RAM available
- A private container registry (important!)

## System Configuration

Increase file descriptor limits for optimal performance:

```bash
# Add to /etc/security/limits.conf
* soft nofile 65535
* hard nofile 65535
```

## Important Tip

**Use a personal image repository during TAP installation.** VMware's Tanzu Registry connections can be unreliable and cause unexplained failures. I recommend using Harbor or another private registry.

## Starting Minikube

TAP requires significant resources:

```bash
minikube start \
  --cpus=8 \
  --memory=14g \
  --kubernetes-version=v1.28.0 \
  --driver=docker
```

## Installing Cluster Essentials

Before TAP, install Tanzu Cluster Essentials:

```bash
# Set environment variables
export INSTALL_BUNDLE=registry.tanzu.vmware.com/tanzu-cluster-essentials/cluster-essentials-bundle:1.7.0
export INSTALL_REGISTRY_HOSTNAME=registry.tanzu.vmware.com
export INSTALL_REGISTRY_USERNAME=your-username
export INSTALL_REGISTRY_PASSWORD=your-password

# Run installation
cd tanzu-cluster-essentials
./install.sh
```

## Installing TAP

1. Create namespace:

```bash
kubectl create namespace tap-install
```

2. Add TAP package repository:

```bash
tanzu package repository add tanzu-tap-repository \
  --url registry.tanzu.vmware.com/tanzu-application-platform/tap-packages:1.7.0 \
  --namespace tap-install
```

3. Install TAP with your values file:

```bash
tanzu package install tap \
  -p tap.tanzu.vmware.com \
  -v 1.7.0 \
  --values-file tap-values.yaml \
  -n tap-install
```

## Deploying Your First Workload

```bash
tanzu apps workload create my-app \
  --git-repo https://github.com/your/app \
  --git-branch main \
  --type web \
  --label app.kubernetes.io/part-of=my-app
```

## Learn More

See my complete installation notes: [tap-install-note](https://github.com/ChunPingWang/tap-install-note)

TAP simplifies the path from code to production on Kubernetes!
