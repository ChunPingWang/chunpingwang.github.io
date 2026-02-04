---
layout: single
title: "Kubernetes 入門指南"
date: 2026-01-28 12:00:00 +0800
categories: [kubernetes, 教學]
tags: [kubernetes, k8s, 容器, devops]
toc: true
toc_sticky: true
---

Kubernetes 已經成為容器編排的業界標準。在這篇文章中，我將分享一些基礎知識幫助你入門。

## 什麼是 Kubernetes？

Kubernetes（K8s）是一個開源的容器編排平台，能夠自動化：

- 容器化應用程式的部署
- 根據需求進行擴展
- 管理容器生命週期
- 負載平衡與服務發現

## 核心概念

### Pods

Kubernetes 中最小的可部署單位。一個 Pod 可以包含一個或多個容器。

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

管理應用程式的期望狀態：

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

對外公開你的應用程式：

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

## 延伸學習

查看我的 [K8sLabs 專案](https://github.com/ChunPingWang/K8sLabs) 獲取更多實戰練習。

祝學習愉快！
