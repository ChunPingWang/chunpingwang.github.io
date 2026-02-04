---
layout: single
title: "E-Commerce Saga Orchestration System"
date: 2026-01-05 12:00:00 +0800
categories: [java, 微服務]
tags: [saga, apache-camel, distributed-transaction, microservices, resilience4j]
toc: true
toc_sticky: true
---

電子商務 Saga 編排系統 - 使用 Saga 模式實現分散式交易的自動補償機制。

## 分支說明

| 分支 | 通訊方式 | 說明 |
|------|----------|------|
| `main` | HTTP 同步 | 使用 HTTP REST 呼叫下游服務 |
| `feature/kafka-cdc` | Kafka 非同步 | Kafka + Debezium CDC 事件驅動架構 |

## 專案狀態

| 階段 | 狀態 | 說明 |
|------|------|------|
| Phase 1-3 | ✅ | 基礎架構、領域模型、端口與適配器 |
| Phase 4 | ✅ | 回滾機制與 Camel 路由 |
| Phase 5 | ✅ | 超時檢測與自動補償 |
| Phase 6 | ✅ | 回滾失敗升級通知 |
| Phase 7 | ✅ | 服務重啟後恢復 |
| Phase 8 | ✅ | 動態服務配置 API |
| Phase 9 | ✅ | 可觀測性與驗收測試 |

## 技術棧

- Java 21
- Spring Boot 3.2.x
- Apache Camel 4.x
- Resilience4j

## 架構特點

- Saga Orchestration Pattern
- 自動補償機制
- 超時檢測
- 可觀測性整合

**Repository:** [saga-camel](https://github.com/ChunPingWang/saga-camel)
