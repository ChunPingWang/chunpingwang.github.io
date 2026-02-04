---
layout: single
title: "CDC PoC - Kafka + Debezium + PostgreSQL"
date: 2026-01-29 15:00:00 +0800
categories: [devops, 資料工程]
tags: [debezium, cdc, kafka, database, postgresql]
toc: true
toc_sticky: true
---

Change Data Capture (CDC) 概念驗證，使用 Debezium 捕獲 PostgreSQL 資料庫變更，透過 Kafka 進行資料串流傳輸。

## 系統架構

```
PostgreSQL A (customers) ──► Debezium ──► Kafka ──► JDBC Sink ──► PostgreSQL Target
PostgreSQL B (orders)    ──► Debezium ──► Kafka ──► JDBC Sink ──►
```

## 系統元件

| 元件 | 版本 | 說明 |
|------|------|------|
| NGINX Ingress | - | 統一流量入口 |
| PostgreSQL Source A | 15 | 客戶資料 |
| PostgreSQL Source B | 15 | 訂單資料 |
| PostgreSQL Target | 15 | 整合資料 |
| Debezium | - | CDC Source Connector |
| Kafka | - | 訊息佇列 |
| JDBC Sink | - | 資料同步 |
| Kafka UI | - | 監控介面 |

## 資料流向

1. PostgreSQL 產生 INSERT/UPDATE/DELETE
2. Debezium 透過 WAL 捕獲變更事件
3. 發布 CDC 事件到 Kafka
4. JDBC Sink 消費訊息
5. 寫入目標資料庫

**端對端延遲 < 1 秒**

**Repository:** [debezium-cdc-poc](https://github.com/ChunPingWang/debezium-cdc-poc)
