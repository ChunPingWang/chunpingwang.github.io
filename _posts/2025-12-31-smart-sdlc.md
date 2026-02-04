---
layout: single
title: "Doc-Pipeline - AI 驅動的文件處理系統"
date: 2025-12-31 14:00:00 +0800
categories: [python, ai]
tags: [ai, llm, document-processing, rag, python]
toc: true
toc_sticky: true
---

AI 驅動的文件處理與規格產出系統，將原始系統設計文件轉換為 AI 可處理的結構化規格。

## 功能特色

| 功能 | 說明 |
|------|------|
| 多格式解析 | Word、Excel、Markdown、PDF、純文字 |
| 智能切分 | 結構/語意/混合策略 |
| LLM 分類 | 自動分類文件內容類型 |
| 向量搜尋 | 語意相似度搜尋 |
| 規格產出 | 需求清單、API 規格、DB Schema |
| 術語檢查 | LLM 驅動的用語規範驗證 |

## 輸出格式

- YAML
- Markdown
- OpenAPI 3.0
- SQL DDL

## LLM 支援

- OpenAI
- Anthropic
- Ollama (本地運行)

## 測試狀態

- 45 個測試通過
- 完整測試覆蓋

**Repository:** [smart-sdlc](https://github.com/ChunPingWang/smart-sdlc)
