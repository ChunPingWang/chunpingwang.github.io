---
layout: single
title: "Resilience4j PoC - 電子商務訂單服務韌性機制"
date: 2026-02-03 12:00:00 +0800
categories: [java, spring]
tags: [resilience4j, circuit-breaker, java, microservices]
toc: true
toc_sticky: true
---

展示如何在微服務架構中實現服務韌性，透過模擬電子商務訂單服務示範三種核心韌性模式。

## 韌性模式

| 模式 | 目的 | 應用場景 |
|------|------|----------|
| **Retry（重試）** | 處理暫時性故障 | 庫存服務網路抖動 |
| **CircuitBreaker（斷路器）** | 防止雪崩效應 | 支付閘道持續故障 |
| **TimeLimiter（超時控制）** | 保護資源不被阻塞 | 物流服務慢回應 |

## In-flight 請求保護機制

- **Graceful Shutdown**：優雅關閉
- **Idempotency**：冪等性設計
- **Outbox Pattern + Saga**：事件驅動架構

## 技術棧

- Java 17+
- Spring Boot 3.2.x
- Resilience4j 2.2.x
- 六角形架構 (Hexagonal Architecture)

## 架構特點

- 完整的 C4 Model 系統架構圖
- 領域模型與狀態機設計
- 分散式交易處理
- 完整測試案例

**Repository:** [resilience4j-poc](https://github.com/ChunPingWang/resilience4j-poc)
