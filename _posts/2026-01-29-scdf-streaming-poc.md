---
layout: single
title: "Spring Cloud Dataflow Streaming PoC"
date: 2026-01-29 23:00:00 +0800
categories: [java, spring]
tags: [spring-cloud-data-flow, streaming, data-pipeline, kafka, kubernetes]
toc: true
toc_sticky: true
---

在 Kind (Kubernetes in Docker) 上運行 Spring Cloud Dataflow 串流處理環境的 PoC 專案。

## 架構元件

| Namespace | 元件 | Port |
|-----------|------|------|
| scdf | Dataflow Server | 9393 → NodePort:30080 |
| scdf | Skipper Server | 7577 → NodePort:30081 |
| scdf | MariaDB | 3306 |
| kafka | Apache Kafka | 9092 → NodePort:30092 |
| ingress-nginx | NGINX Ingress | 80, 443 |

## 資料流架構

```
Source App → Kafka → Processor App → Kafka → Sink App
```

## 主要功能

- **Dataflow Server**：串流管理與部署
- **Skipper Server**：應用程式版本管理
- **Kafka**：訊息傳遞
- **MariaDB**：中繼資料儲存
- **NGINX Ingress**：流量入口

## 環境需求

- Kind (Kubernetes in Docker)
- kubectl
- Docker

**Repository:** [scdf-streaming-poc](https://github.com/ChunPingWang/scdf-streaming-poc)
