---
layout: single
title: "Harbor 容器映像倉庫安裝與設定"
date: 2026-02-04 12:00:00 +0800
categories: [devops, 容器]
tags: [harbor, docker, registry, kubernetes, 憑證]
toc: true
toc_sticky: true
---

Harbor 是一個開源的容器映像倉庫，提供安全掃描、映像簽章和角色型存取控制等重要功能。本文將分享如何使用自簽憑證設定 Harbor。

## 為什麼選擇 Harbor？

在開發環境或隔離網路環境中使用 Kubernetes 時，你需要一個私有容器倉庫。Harbor 提供：

- **安全掃描** - 檢測漏洞
- **映像複製** - 跨倉庫同步
- **角色型存取控制** - 權限管理
- **稽核日誌** - 操作記錄
- **Helm Chart 倉庫** - 圖表管理

## 產生自簽憑證

首先，為 Harbor 建立 SSL 憑證：

```bash
# 產生 CA 憑證
openssl genrsa -out ca.key 4096
openssl req -x509 -new -nodes -sha512 -days 3650 \
  -subj "/CN=harbor-ca" \
  -key ca.key \
  -out ca.crt

# 產生伺服器憑證
openssl genrsa -out harbor.key 4096
openssl req -sha512 -new \
  -subj "/CN=harbor.example.com" \
  -key harbor.key \
  -out harbor.csr

# 簽署憑證
openssl x509 -req -sha512 -days 3650 \
  -CA ca.crt -CAkey ca.key -CAcreateserial \
  -in harbor.csr \
  -out harbor.crt
```

## 設定 Docker 信任憑證

### Linux 系統

```bash
sudo mkdir -p /etc/docker/certs.d/harbor.example.com
sudo cp ca.crt /etc/docker/certs.d/harbor.example.com/
sudo systemctl restart docker
```

### macOS 系統

```bash
sudo security add-trusted-cert -d -r trustRoot \
  -k /Library/Keychains/System.keychain ca.crt
# 重新啟動 Docker Desktop
```

### Minikube 環境

```bash
minikube start --insecure-registry="harbor.example.com"
# 或將憑證複製到 minikube
minikube cp ca.crt /etc/docker/certs.d/harbor.example.com/ca.crt
```

## 安裝 Harbor

1. 從 [Harbor releases](https://github.com/goharbor/harbor/releases) 下載
2. 解壓縮並設定 `harbor.yml`：

```yaml
hostname: harbor.example.com
https:
  port: 443
  certificate: /path/to/harbor.crt
  private_key: /path/to/harbor.key
harbor_admin_password: YourSecurePassword
```

3. 執行安裝程式：

```bash
./install.sh --with-trivy
```

## 延伸閱讀

查看我的詳細筆記：[harbor-install-note](https://github.com/ChunPingWang/harbor-install-note)

Harbor 是任何正式 Kubernetes 部署的必備工具，值得花時間好好設定！
