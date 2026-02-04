---
layout: single
title: "Spring Boot Learning - 從基礎到企業級安全"
date: 2026-01-17 15:00:00 +0800
categories: [java, spring]
tags: [spring-boot, java, learning, spring-security]
toc: true
toc_sticky: true
---

Spring Boot 學習專案，採用 Gradle 多模組架構，從基礎概念到企業級安全實作。

## Spring 發展歷程

| 年份 | 里程碑 |
|------|--------|
| 2004 | Spring Framework 1.0 發布 |
| 2014 | Spring Boot 1.0 發布 ⭐ |
| 2017 | Spring 5.0：響應式編程 |
| 2022 | Spring Boot 3.0：Jakarta EE 9+ |

## 為什麼選擇 Spring？

| 傳統 Java EE 問題 | Spring 解決方案 |
|------------------|------------------|
| 大量 XML 配置 | 註解驅動 + 自動配置 |
| 程式碼與框架耦合 | IoC/DI 實現鬆耦合 |
| 測試困難 | 內建測試支援 |
| 部署複雜 | 內嵌伺服器，獨立運行 |

## 專案結構

```
spring-boot-learning/
├── spring-boot-basics/      # 模組一：Spring Boot 基礎
│   ├── README.md            # 教學文件（8 章節）
│   └── ANNOTATIONS.md       # 註解參考手冊
├── spring-security-demo/    # 模組二：Spring Security
│   ├── README.md
│   └── SECURITY.md          # 教學文件（6 章節）
```

## Spring 核心概念

- **IoC 容器**：控制反轉
- **DI**：依賴注入
- **AOP**：切面導向程式設計
- **自動配置**：約定優於配置
- **Starter 依賴**：快速整合
- **內嵌伺服器**：獨立運行

**Repository:** [spring-boot-learning](https://github.com/ChunPingWang/spring-boot-learning)
