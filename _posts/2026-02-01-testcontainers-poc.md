---
layout: single
title: "Testcontainers 企業級整合測試解決方案"
date: 2026-02-01 14:00:00 +0800
categories: [java, 測試]
tags: [testcontainers, java, testing, docker, integration-test]
toc: true
toc_sticky: true
---

企業級金融系統整合測試解決方案，使用 Testcontainers 框架實現環境隔離的自動化測試。

## 測試金字塔

```
🔺 E2E / UI 測試 (10%)
🔷 整合測試 (20%) ← 本專案重點
🟩 單元測試 (70%)
```

## 測試層級比較

| 層級 | 執行速度 | 維護成本 | 建議比例 |
|------|----------|----------|----------|
| 單元測試 | 毫秒級 | 低 | 70% |
| 整合測試 | 秒級 | 中 | 20% |
| E2E 測試 | 分鐘級 | 高 | 10% |

## FIRST 原則

- **F**ast（快速）
- **I**ndependent（獨立）
- **R**epeatable（可重複）
- **S**elf-Validating（自我驗證）
- **T**imely（及時）

## AAA 測試模式

```java
@Test
void shouldCalculateOrderTotal() {
    // Arrange（準備）
    // Act（執行）
    // Assert（斷言）
}
```

**Repository:** [testcontainers-poc](https://github.com/ChunPingWang/testcontainers-poc)
