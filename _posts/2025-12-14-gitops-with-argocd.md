---
layout: single
title: "GitOps with ArgoCD - Spring PetClinic 部署"
date: 2025-12-14 12:00:00 +0800
categories: [devops, kubernetes]
tags: [gitops, argocd, kubernetes, spring-petclinic]
toc: true
toc_sticky: true
---

使用 GitOps 方法，透過 ArgoCD 將 Spring PetClinic 微服務應用程式部署到 Kubernetes。

## 架構元件

### ArgoCD Namespace
- ArgoCD Server
- ArgoCD Repo Server
- ArgoCD Application Controller

### PetClinic Namespace
- API Gateway (:8080)
- Customers Service (:8081)
- Visits Service (:8082)
- Vets Service (:8083)
- GenAI Service (:8084)
- MySQL (:3306)
- Zipkin Tracing (:9411)
- Prometheus (:9090)
- Grafana (:3000)

## 學習內容

1. 建立 Kind Cluster
2. 安裝 ArgoCD
3. 存取 ArgoCD UI
4. 建置應用程式映像檔
5. 部署 PetClinic 應用程式
6. 驗證部署

## 技術棧

- Kind (Kubernetes in Docker)
- ArgoCD
- Spring PetClinic
- Prometheus + Grafana

**Repository:** [gitops-with-argocd](https://github.com/ChunPingWang/gitops-with-argocd)
