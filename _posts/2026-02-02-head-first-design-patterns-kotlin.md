---
layout: single
title: "Head First Design Patterns - Kotlin 現代化實作"
date: 2026-02-02 16:00:00 +0800
categories: [kotlin, 設計模式]
tags: [design-pattern, kotlin, oop]
toc: true
toc_sticky: true
---

《深入淺出設計模式》一書的 Kotlin 現代化實作版本，充分利用 Kotlin 的語言特性，讓設計模式的實作更加簡潔優雅。

## 專案特點

- **完整覆蓋**：涵蓋書中所有 23 種 GoF 設計模式
- **現代 Kotlin**：使用 Kotlin 2.x 和最新語言特性
- **中文說明**：詳細的中文教學文檔
- **TDD 導向**：採用測試驅動開發

## Kotlin vs Java 實作優勢

| 設計模式 | Java | Kotlin | 優勢 |
|----------|------|--------|------|
| 單例模式 | 雙重檢查鎖定 | `object` 宣告 | 線程安全、簡潔 |
| 裝飾者模式 | 裝飾器類層次 | `by` 委託 | 減少樣板程式碼 |
| 策略模式 | 介面 + 實作類 | Lambda | 更加簡潔 |
| 狀態模式 | 狀態介面 | `sealed class` | 類型安全 |
| 建造者模式 | Builder 內部類 | DSL | 無需額外類別 |

## 涵蓋模式

- 創建型模式：Singleton, Factory, Builder, Prototype
- 結構型模式：Adapter, Decorator, Facade, Proxy
- 行為型模式：Strategy, Observer, Command, State

**Repository:** [head-first-design-patterns-kotlin](https://github.com/ChunPingWang/head-first-design-patterns-kotlin)
