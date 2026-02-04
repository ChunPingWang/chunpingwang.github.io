---
layout: single
title: "Circuit Breaker Microservices"
date: 2025-12-04 12:00:00 +0800
categories: [java, 微服務]
tags: [circuit-breaker, microservices, resilience, hexagonal-architecture]
toc: true
toc_sticky: true
---

具備斷路器韌性機制的微服務架構範例專案。

## 服務架構

| 服務 | 說明 |
|------|------|
| mp-service | 主服務，協調下游服務並實作斷路器 |
| gbp-service | 時間提供服務 |
| gin-service | 時間接收服務 |

## 主要特色

- **斷路器模式**：Circuit Breaker Pattern
- **服務降級**：資料暫存機制
- **自動恢復**：資料補發
- **六角形架構**：Hexagonal Architecture
- **Swagger API 文件**

## 運作機制

當 gin-service 無法連線時：
1. mp-service 將資料暫存至資料庫
2. 待服務恢復後自動補發
3. 確保資料不遺失

**Repository:** [circuit-breaker](https://github.com/ChunPingWang/circuit-breaker)
