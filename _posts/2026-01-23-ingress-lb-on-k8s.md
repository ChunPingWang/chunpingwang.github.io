---
layout: single
title: "Kubernetes Ingress 與 LoadBalancer 教學"
date: 2026-01-23 02:00:00 +0800
categories: [kubernetes]
tags: [kubernetes, ingress, load-balancer, networking, kind]
toc: true
toc_sticky: true
---

了解 Kubernetes 中兩種常見的流量入口方式：Ingress 和 LoadBalancer。

## Service 類型比較

| 類型 | 說明 | 比喻 |
|------|------|------|
| **ClusterIP** | 只能在叢集內部存取 | 公司內部分機號碼 |
| **NodePort** | 在每個節點上開放端口 | 每棟大樓都開後門 |
| **LoadBalancer** | 取得外部 IP | 請專人在門口接待 |

## Ingress 是什麼？

Ingress 就像是聰明的接待員，可以根據：
- **URL 路徑**：`/apple` → A 服務，`/banana` → B 服務
- **主機名稱**：`shop.example.com` → 購物，`blog.example.com` → 部落格

## Ingress vs LoadBalancer

| 特性 | Ingress | LoadBalancer |
|------|---------|--------------|
| 層級 | L7 (HTTP/HTTPS) | L4 (TCP/UDP) |
| IP 數量 | 一個 IP 多服務 | 每服務一個 IP |
| 路由能力 | 路徑/域名路由 | 無 |
| 成本 | 較低 | 較高 |

## 環境需求

- Docker
- Kind (Kubernetes in Docker)
- kubectl

## 使用情境

- **只需 Ingress**：Web 應用、HTTP API
- **只需 LoadBalancer**：資料庫、非 HTTP 服務
- **兩者都需要**：企業級架構

**Repository:** [ingress-lb-on-k8s](https://github.com/ChunPingWang/ingress-lb-on-k8s)
