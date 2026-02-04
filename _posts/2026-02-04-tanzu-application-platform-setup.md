---
layout: single
title: "在 Minikube 上安裝 Tanzu Application Platform"
date: 2026-02-04 13:00:00 +0800
categories: [devops, kubernetes]
tags: [tanzu, tap, vmware, kubernetes, minikube, 平台工程]
toc: true
toc_sticky: true
---

Tanzu Application Platform（TAP）是 VMware 基於 Kubernetes 打造的開發者平台，提供完整的應用程式建置與部署工具鏈。本文介紹如何在本地 minikube 叢集上設定 TAP。

## 前置需求

- Ubuntu Desktop（或類似的 Linux 發行版）
- 已安裝 Minikube
- 至少 16GB 可用記憶體
- 私有容器倉庫（重要！）

## 系統設定

增加檔案描述符限制以獲得最佳效能：

```bash
# 新增至 /etc/security/limits.conf
* soft nofile 65535
* hard nofile 65535
```

## 重要提示

**在安裝 TAP 時請使用私人映像倉庫。** VMware 的 Tanzu Registry 連線可能不穩定，導致無法解釋的失敗。我建議使用 Harbor 或其他私有倉庫。

## 啟動 Minikube

TAP 需要大量資源：

```bash
minikube start \
  --cpus=8 \
  --memory=14g \
  --kubernetes-version=v1.28.0 \
  --driver=docker
```

## 安裝 Cluster Essentials

在安裝 TAP 之前，先安裝 Tanzu Cluster Essentials：

```bash
# 設定環境變數
export INSTALL_BUNDLE=registry.tanzu.vmware.com/tanzu-cluster-essentials/cluster-essentials-bundle:1.7.0
export INSTALL_REGISTRY_HOSTNAME=registry.tanzu.vmware.com
export INSTALL_REGISTRY_USERNAME=your-username
export INSTALL_REGISTRY_PASSWORD=your-password

# 執行安裝
cd tanzu-cluster-essentials
./install.sh
```

## 安裝 TAP

1. 建立命名空間：

```bash
kubectl create namespace tap-install
```

2. 新增 TAP 套件倉庫：

```bash
tanzu package repository add tanzu-tap-repository \
  --url registry.tanzu.vmware.com/tanzu-application-platform/tap-packages:1.7.0 \
  --namespace tap-install
```

3. 使用你的設定檔安裝 TAP：

```bash
tanzu package install tap \
  -p tap.tanzu.vmware.com \
  -v 1.7.0 \
  --values-file tap-values.yaml \
  -n tap-install
```

## 部署你的第一個應用程式

```bash
tanzu apps workload create my-app \
  --git-repo https://github.com/your/app \
  --git-branch main \
  --type web \
  --label app.kubernetes.io/part-of=my-app
```

## 延伸閱讀

查看我的完整安裝筆記：[tap-install-note](https://github.com/ChunPingWang/tap-install-note)

TAP 簡化了從程式碼到 Kubernetes 生產環境的流程！
