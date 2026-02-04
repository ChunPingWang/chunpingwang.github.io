---
layout: single
title: "Kubernetes 實戰練習：從零到生產"
date: 2026-02-04 15:00:00 +0800
categories: [kubernetes, 教學]
tags: [kubernetes, k8s, kind, 容器, devops, 實作]
toc: true
toc_sticky: true
---

學習 Kubernetes 需要實際動手練習。我建立了 K8sLabs 工作坊，透過實戰練習幫助你掌握 Kubernetes 基礎。

## 為什麼需要 Kubernetes？

Kubernetes 源自 Google 內部的 Borg 系統，已經在大規模環境中管理容器超過十年。今天，K8s 是以下領域的業界標準：

- 容器編排
- 自我修復部署
- 水平擴展
- 服務發現
- 組態管理

## 使用 Kind 建立本地叢集

Kind（Kubernetes in Docker）非常適合學習：

```bash
# 安裝 kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# 建立多節點叢集
cat <<EOF | kind create cluster --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
EOF
```

## 涵蓋的核心概念

### 1. Namespaces（命名空間）

組織和隔離資源：

```bash
kubectl create namespace dev
kubectl create namespace prod
kubectl get namespaces
```

### 2. Pods

最小的可部署單位：

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

### 3. Multi-Container Pods（多容器 Pod）

同一個 Pod 中的容器共享網路和儲存：

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

### 4. Deployments（部署）

管理副本和更新：

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

### 5. Jobs 與 CronJobs

批次處理：

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

### 6. Services（服務）

Pod 的網路抽象：

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

## 工作坊結構

實驗從基礎到進階逐步推進：

1. 使用 Vagrant/Kind 設定環境
2. Namespace 和資源組織
3. Pod 生命週期管理
4. 部署策略
5. Service 網路
6. ConfigMaps 和 Secrets
7. 持久化儲存

## 開始學習

Clone 專案並跟著練習：[K8sLabs](https://github.com/ChunPingWang/K8sLabs)

學習 Kubernetes 最好的方式就是動手做。從實驗開始，建立你的信心！
