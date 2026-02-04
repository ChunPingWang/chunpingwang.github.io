---
layout: single
title: "Nexus Repository 地端部署方案"
date: 2026-02-02 14:00:00 +0800
categories: [devops, container]
tags: [nexus, docker, repository, artifacts, maven]
toc: true
toc_sticky: true
---

Sonatype Nexus Repository Community Edition 的 Docker 部署方案，適用於企業內部套件管理。

## 架構元件

| 容器 | Image | 用途 |
|------|-------|------|
| nexus | sonatype/nexus3:3.88.0 | Nexus Repository Manager |
| nginx | nginx:1.27-alpine | TLS 終止、反向代理 |
| backup | alpine:3.21 | 定時備份 (每日 02:00) |

## 主要功能

- Maven Repository 代理與託管
- TLS/HTTPS 安全連線
- 自動備份機制
- Prometheus 監控整合

## Repository 類型

```
maven-public (group)
├── maven-releases (hosted)
├── maven-snapshots (hosted)
└── maven-central-proxy (proxy)
```

## 系統需求

| 項目 | 最低需求 | 建議 |
|------|---------|------|
| CPU | 4 cores | 8 cores |
| 記憶體 | 8 GB | 16 GB |
| 磁碟 | 50 GB | 100 GB+ SSD |

**Repository:** [nexus-repository-docker](https://github.com/ChunPingWang/nexus-repository-docker)
