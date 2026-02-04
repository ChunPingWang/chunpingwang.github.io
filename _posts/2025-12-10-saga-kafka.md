---
layout: single
title: "Saga-Kafka 分散式交易系統"
date: 2025-12-10 12:00:00 +0800
categories: [java, 微服務]
tags: [saga, kafka, distributed-transaction, microservices, ddd]
toc: true
toc_sticky: true
---

使用 Saga 編排模式 (Orchestration Pattern) 實作的分散式交易系統，透過 Apache Kafka 進行微服務間的非同步通訊。

## 架構特點

- **Saga 編排模式**：Order Service 作為 Orchestrator
- **Clean Architecture**：六角形架構
- **DDD**：領域驅動設計
- **Kafka**：非同步訊息通訊

## 主要功能

- 成功流程處理
- 失敗補償流程
- 超時處理
- 競態條件處理
- 自動重試機制

## Kafka 設計

- Topic 設計原則
- 訊息格式規範
- 可靠性保證
- 冪等性處理

## 可觀測性

- 分散式追蹤
- 指標監控
- 日誌聚合

**Repository:** [saga-kafka](https://github.com/ChunPingWang/saga-kafka)
