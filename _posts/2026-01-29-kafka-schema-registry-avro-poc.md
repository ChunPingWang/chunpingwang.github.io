---
layout: single
title: "Kafka + Schema Registry + Avro 微服務 PoC"
date: 2026-01-29 16:00:00 +0800
categories: [java, kafka]
tags: [kafka, schema-registry, avro, streaming, microservices]
toc: true
toc_sticky: true
---

展示兩個微服務透過 Kafka 事件驅動架構傳遞資料，並完整呈現 Schema Registry 多版本管理與 ksqlDB 即時監控能力。

## 專案重點

- **事件驅動架構**：Order Service (Producer) 和 Inventory Service (Consumer)
- **Schema 版本管理**：Confluent Schema Registry 管理 Avro Schema
- **即時監控**：ksqlDB 即時串流查詢和延遲監控
- **視覺化管理**：AKHQ 提供 Kafka 叢集管理介面

## Avro vs 其他格式

| 特性 | JSON | Protocol Buffers | Avro |
|------|------|------------------|------|
| 格式 | 文字 | 二進位 | 二進位 |
| Schema | 無 | 必須 (.proto) | 必須 (.avsc) |
| 大小 | 大 | 小 | 最小 |
| Schema 演進 | 困難 | 支援 | 最佳支援 |

## Avro 資料類型

**原始類型：** null, boolean, int, long, float, double, bytes, string

**複雜類型：** record, enum, array, map, union, fixed

## Schema 演進

支援向前/向後相容性，允許 Schema 隨時間變化。

**Repository:** [kafka-schema-registry-avro-poc](https://github.com/ChunPingWang/kafka-schema-registry-avro-poc)
