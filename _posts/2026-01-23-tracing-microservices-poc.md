---
layout: single
title: "天氣查詢可觀測性展示系統"
date: 2026-01-23 16:00:00 +0800
categories: [devops, 微服務]
tags: [tracing, microservices, observability, jaeger, opentelemetry, prometheus, grafana]
toc: true
toc_sticky: true
---

一個完整的分散式追蹤與可觀測性實作範例，透過天氣查詢應用程式展示現代微服務架構的最佳實踐。

## 學習目標

- 分散式追蹤
- 可觀測性三大支柱
- Trace ID 與 Span ID 概念
- OpenTelemetry、Jaeger、Prometheus、Grafana 整合

## 主要功能

| 功能 | 說明 |
|------|------|
| 天氣查詢 | 台北、台中、高雄三城市天氣 |
| 追蹤視覺化 | Jaeger UI 查看完整請求鏈路 |
| 指標儀表板 | Grafana 監控系統指標 |
| Swagger UI | 互動式 API 文件與測試 |
| H2 Console | 瀏覽器內資料庫管理 |

## 技術棧

- Java 17+
- Node.js 18+
- Docker & Docker Compose
- Gradle 8.x
- OpenTelemetry
- Jaeger
- Prometheus
- Grafana
- Micrometer

## 可觀測性三大支柱

1. **Logs（日誌）**：記錄事件
2. **Metrics（指標）**：量化監控
3. **Traces（追蹤）**：請求鏈路

**Repository:** [tracing-microservices-poc](https://github.com/ChunPingWang/tracing-microservices-poc)
