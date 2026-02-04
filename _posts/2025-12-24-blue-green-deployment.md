---
layout: single
title: "藍綠佈署展示專案"
date: 2025-12-24 16:00:00 +0800
categories: [devops, kubernetes]
tags: [blue-green, deployment, spring-cloud-gateway, kubernetes]
toc: true
toc_sticky: true
---

使用 Spring Cloud Gateway 實現藍綠佈署（Blue-Green Deployment）的微服務展示專案。

## 分支說明

| 分支 | 說明 |
|------|------|
| `main` | 本機開發版本 |
| `deploy-on-k8s` | Kubernetes 部署版本 |

## 架構說明

```
                    ┌─────────────────┐
                    │   API Gateway   │
                    │  (Port: 8080)   │
                    └────────┬────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼ 20%                         ▼ 80%
    ┌─────────────────┐           ┌─────────────────┐
    │  Blue Service   │           │  Green Service  │
    │  (Port: 8081)   │           │  (Port: 8082)   │
    └─────────────────┘           └─────────────────┘
```

## 主要功能

- 安全地進行版本切換
- 漸進式發布新功能
- 快速回滾至穩定版本
- A/B 測試

## 技術棧

- Spring Cloud Gateway
- 加權路由
- Docker / Kubernetes

**Repository:** [blue-green-deployment](https://github.com/ChunPingWang/blue-green-deployment)
