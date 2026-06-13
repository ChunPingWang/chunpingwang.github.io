---
title: "專案總覽"
layout: single
permalink: /projects/
author_profile: true
toc: true
toc_sticky: true
---

這裡依主題分類整理我在 GitHub 上公開分享的專案、教學與概念驗證 (PoC)。每個專案在部落格中也有對應的文章，點擊即可前往 GitHub 原始碼。

> 分類原則：僅收錄**公開**且具完整內容的儲存庫；排除私有專案、暫存／測試用儲存庫與網站原始碼本身。

## ☁️ Kubernetes / 雲端原生

容器編排、服務網格、API Gateway、備份遷移與叢集建置。

- [k8s-install-with-kubeadm](https://github.com/ChunPingWang/k8s-install-with-kubeadm) — kubeadm 安裝 Kubernetes
- [K8s-tutorial-with-kind](https://github.com/ChunPingWang/K8s-tutorial-with-kind) — Kind 本地測試叢集
- [istio-tutorial](https://github.com/ChunPingWang/istio-tutorial) — Istio 服務網格
- [kubevirt-tutorial](https://github.com/ChunPingWang/kubevirt-tutorial) — KubeVirt 虛擬機
- [dapr-tutorial](https://github.com/ChunPingWang/dapr-tutorial) — Dapr 分散式執行環境
- [ingress-vs-gateway-api-tutorial](https://github.com/ChunPingWang/ingress-vs-gateway-api-tutorial) — Ingress vs Gateway API
- [apisix-poc](https://github.com/ChunPingWang/apisix-poc) — Apache APISIX API Gateway
- [terraform-for-podman-k8s-tutorial](https://github.com/ChunPingWang/terraform-for-podman-k8s-tutorial) — Terraform 佈建 Podman/K8s
- [rancher-k8s-tutorial](https://github.com/ChunPingWang/rancher-k8s-tutorial) — Rancher 叢集管理
- [nutanix-k8s-platform-tutorial](https://github.com/ChunPingWang/nutanix-k8s-platform-tutorial) — Nutanix K8s 平台
- [openshift-local-tutorial](https://github.com/ChunPingWang/openshift-local-tutorial) · [openshift-learning](https://github.com/ChunPingWang/openshift-learning) — OpenShift
- [buildpack-tutorial](https://github.com/ChunPingWang/buildpack-tutorial) — Cloud Native Buildpacks
- [k8s-backup-velero-poc](https://github.com/ChunPingWang/k8s-backup-velero-poc) · [k8s-backup-k10-poc](https://github.com/ChunPingWang/k8s-backup-k10-poc) — 備份遷移
- [ckx-preparation](https://github.com/ChunPingWang/ckx-preparation) — CKA/CKAD/CKS 認證準備

## 🌱 Spring / Java

Spring Boot、Spring Cloud、全端整合與 PetClinic 系列。

- [spring-boot2-tutorial](https://github.com/ChunPingWang/spring-boot2-tutorial) — Spring Boot 2
- [spring-ai-tutorial](https://github.com/ChunPingWang/spring-ai-tutorial) · [spring-ai-recipes-pratices](https://github.com/ChunPingWang/spring-ai-recipes-pratices) — Spring AI
- [springboot-reactjs-tutorial](https://github.com/ChunPingWang/springboot-reactjs-tutorial) · [vue-spring-boot2-tutorial](https://github.com/ChunPingWang/vue-spring-boot2-tutorial) — 全端整合
- [mybatis-tutorial](https://github.com/ChunPingWang/mybatis-tutorial) — MyBatis ORM
- [graphql-tutorial](https://github.com/ChunPingWang/graphql-tutorial) — GraphQL
- [spring-cloud-contract-tutorial](https://github.com/ChunPingWang/spring-cloud-contract-tutorial) · [spring-cloud-contract2-tutorial](https://github.com/ChunPingWang/spring-cloud-contract2-tutorial) — 契約測試
- [spring-petclinic-learning](https://github.com/ChunPingWang/spring-petclinic-learning) · [spring-petclinic-modulith](https://github.com/ChunPingWang/spring-petclinic-modulith) · [spring-petclinic-microservices](https://github.com/ChunPingWang/spring-petclinic-microservices) — PetClinic 系列

## 🧩 設計模式 / OOP / 架構

設計模式、SOLID、Clean Architecture、DDD 與重構。

- [solid-principles-tutorial](https://github.com/ChunPingWang/solid-principles-tutorial) — SOLID 原則
- [solid-hexagonal-cqrs-tutorial](https://github.com/ChunPingWang/solid-hexagonal-cqrs-tutorial) — 六角形架構 + CQRS
- [gof-design-patterns-dotnet-core](https://github.com/ChunPingWang/gof-design-patterns-dotnet-core) — GoF 設計模式
- [ddd-design-patterns-tutorial](https://github.com/ChunPingWang/ddd-design-patterns-tutorial) — DDD 設計模式
- [clean_architecture_with_Spring](https://github.com/ChunPingWang/clean_architecture_with_Spring) — Clean Architecture
- [dependency-injection-tutorial-](https://github.com/ChunPingWang/dependency-injection-tutorial-) · [dotnet-core-10-dependecy-injection](https://github.com/ChunPingWang/dotnet-core-10-dependecy-injection) — 依賴注入
- [refactoring-bad-smells-java](https://github.com/ChunPingWang/refactoring-bad-smells-java) · [-dotnet](https://github.com/ChunPingWang/refactoring-bad-smells-dotnet) · [-javascript](https://github.com/ChunPingWang/refactoring-bad-smells-javascript) — 重構壞味道
- [circuit-breaker-pattern](https://github.com/ChunPingWang/circuit-breaker-pattern) — 斷路器模式四語言比較
- [six-api-architecture-styles-tutorial](https://github.com/ChunPingWang/six-api-architecture-styles-tutorial) · [12-architecture-concepts](https://github.com/ChunPingWang/12-architecture-concepts) — 架構概念

## 🔗 微服務 / 訊息

事件驅動、Saga、訊息佇列與服務治理。

- [event-driven-microservices](https://github.com/ChunPingWang/event-driven-microservices) — 事件驅動微服務
- [kafka-vs-rabbitmq-tutorial](https://github.com/ChunPingWang/kafka-vs-rabbitmq-tutorial) — Kafka vs RabbitMQ
- [saga-with-mass-transit-tutorial](https://github.com/ChunPingWang/saga-with-mass-transit-tutorial) — Saga (MassTransit)
- [nacos-poc](https://github.com/ChunPingWang/nacos-poc) · [nacos1.x-poc](https://github.com/ChunPingWang/nacos1.x-poc) — Nacos 服務發現
- [service-2-service-comm-in-backend](https://github.com/ChunPingWang/service-2-service-comm-in-backend) — 服務間通訊
- [order-example](https://github.com/ChunPingWang/order-example) — 零售業微服務範例
- [microfoundry_tutorial](https://github.com/ChunPingWang/microfoundry_tutorial) · [microfoundry_poc](https://github.com/ChunPingWang/microfoundry_poc) — MicroFoundry

## 🗄️ 資料 / 資料庫

關聯式、NoSQL、快取、MPP 分析與串流。

- [postgresql17-tutorial](https://github.com/ChunPingWang/postgresql17-tutorial) — PostgreSQL 17
- [mongodb-tutorial](https://github.com/ChunPingWang/mongodb-tutorial) — MongoDB
- [redis-tutorial](https://github.com/ChunPingWang/redis-tutorial) — Redis
- [caching-tutorial](https://github.com/ChunPingWang/caching-tutorial) · [5-caching-strategies-with-redis-tutorial](https://github.com/ChunPingWang/5-caching-strategies-with-redis-tutorial) — 快取策略
- [enterprise-redis-caching-design-java](https://github.com/ChunPingWang/enterprise-redis-caching-design-java) · [-dotnet](https://github.com/ChunPingWang/enterprise-redis-caching-design-dotnet) — 企業快取設計
- [cloudberry-tutorial](https://github.com/ChunPingWang/cloudberry-tutorial) — Cloudberry MPP
- [apache-flink-tutorial](https://github.com/ChunPingWang/apache-flink-tutorial) — Flink 串流
- [datalake-with-minio-and-iceberg-tutorial](https://github.com/ChunPingWang/datalake-with-minio-and-iceberg-tutorial) — MinIO + Iceberg 資料湖

## 🤖 AI / ML / LLM

LLM、RAG、MLOps、邊緣 AI 與機器學習。

- [spring-ai-recipes-pratices](https://github.com/ChunPingWang/spring-ai-recipes-pratices) — Spring AI 食譜
- [llm-rag-tutroial](https://github.com/ChunPingWang/llm-rag-tutroial) · [rag-practices-with-claude](https://github.com/ChunPingWang/rag-practices-with-claude) — RAG
- [mcp_skill_tutorial](https://github.com/ChunPingWang/mcp_skill_tutorial) — MCP Skill
- [mlops-llmops-agentops-tutorial](https://github.com/ChunPingWang/mlops-llmops-agentops-tutorial) — MLOps/LLMOps/AgentOps
- [machine-learning-tutorial](https://github.com/ChunPingWang/machine-learning-tutorial) · [scikit-tutorial](https://github.com/ChunPingWang/scikit-tutorial) · [pytorach-tutorial](https://github.com/ChunPingWang/pytorach-tutorial) — 機器學習 / 深度學習
- [cuda-tutorial-for-jetson](https://github.com/ChunPingWang/cuda-tutorial-for-jetson) · [pytorch-tutorial-for-jetson](https://github.com/ChunPingWang/pytorch-tutorial-for-jetson) · [yolo-tutorial-for-jetson](https://github.com/ChunPingWang/yolo-tutorial-for-jetson) — Jetson 邊緣 AI
- [gemma-4-26b-trail-run](https://github.com/ChunPingWang/gemma-4-26b-trail-run) — 本地量化模型試跑

## 🔌 嵌入式 / 機器人 / 控制

微控制器、感測器、IMU、飛控與控制理論。

- [stm32-tutorial](https://github.com/ChunPingWang/stm32-tutorial) · [ministm32-tutorial](https://github.com/ChunPingWang/ministm32-tutorial) — STM32
- [mcu-20948-poc](https://github.com/ChunPingWang/mcu-20948-poc) · [pico-20948-poc](https://github.com/ChunPingWang/pico-20948-poc) — ICM-20948 9 軸 IMU
- [arduino-gps-ins-tutorial](https://github.com/ChunPingWang/arduino-gps-ins-tutorial) — GPS/INS
- [pid-kalman-filter-tutorial](https://github.com/ChunPingWang/pid-kalman-filter-tutorial) — PID / Kalman Filter
- [drone-flight-control-poc](https://github.com/ChunPingWang/drone-flight-control-poc) · [water-rocket-flight-control-tutorial](https://github.com/ChunPingWang/water-rocket-flight-control-tutorial) — 飛行控制
- [free-rtos-example](https://github.com/ChunPingWang/free-rtos-example) — FreeRTOS

## 🔧 DevOps / 平台 / 工具

IaC、CI/CD、可觀測性、開發者平台與 AI 輔助開發。

- [docker-basic](https://github.com/ChunPingWang/docker-basic) — Docker 基礎
- [terraform-blue-green-tutorial](https://github.com/ChunPingWang/terraform-blue-green-tutorial) — Terraform 藍綠部署
- [backstage-tutorial-](https://github.com/ChunPingWang/backstage-tutorial-) · [ai-ops-backstage](https://github.com/ChunPingWang/ai-ops-backstage) — Backstage / AIOps
- [tracing-otel-agent-poc](https://github.com/ChunPingWang/tracing-otel-agent-poc) — OpenTelemetry 追蹤
- [ibm-bob-tutorial](https://github.com/ChunPingWang/ibm-bob-tutorial) · [ibm-bob-for-sdlc](https://github.com/ChunPingWang/ibm-bob-for-sdlc) · [spec-driven-development-with-bob](https://github.com/ChunPingWang/spec-driven-development-with-bob) — AI 輔助 SDLC
- [github-copilot-workshop-java](https://github.com/ChunPingWang/github-copilot-workshop-java) · [-csharp](https://github.com/ChunPingWang/github-copilot-workshop-csharp) — GitHub Copilot

## ✅ 測試 / 品質

契約測試、架構測試、E2E、BDD 與 Kata。

- [better-microservice-testing](https://github.com/ChunPingWang/better-microservice-testing) — 微服務測試策略
- [taikai-tutorial-](https://github.com/ChunPingWang/taikai-tutorial-) — 架構守護測試
- [playwright-poc](https://github.com/ChunPingWang/playwright-poc) — E2E 測試
- [docs-to-testcases](https://github.com/ChunPingWang/docs-to-testcases) — 文件轉測試案例
- [sdd-for-tennis-kata](https://github.com/ChunPingWang/sdd-for-tennis-kata) · [sdd-for-bowling-kata](https://github.com/ChunPingWang/sdd-for-bowling-kata) — SDD Kata

## 🔐 資安

驗證授權、RBAC、SSO 與 JWT。

- [jwt-poc](https://github.com/ChunPingWang/jwt-poc) · [JWT-tutorial](https://github.com/ChunPingWang/JWT-tutorial) — JWT
- [rbac-sso-tutorial-with-openspec](https://github.com/ChunPingWang/rbac-sso-tutorial-with-openspec) — RBAC / SSO

## 💻 程式語言基礎

語言入門與工程數學。

- [c-lang-pointer-tutorial](https://github.com/ChunPingWang/c-lang-pointer-tutorial) — C 指標
- [cpp-tutorial](https://github.com/ChunPingWang/cpp-tutorial) — C++
- [matlab-tutorial](https://github.com/ChunPingWang/matlab-tutorial) — MATLAB
- [engineering-linalg-tutorial](https://github.com/ChunPingWang/engineering-linalg-tutorial) — 工程線性代數

## 🔒 私有專案

以下為**私有 (Private)** 儲存庫，未公開原始碼，因此不提供連結。內容多為企業／客戶領域系統、認證練習與內部 PoC。

> 若你對其中專案有興趣或有合作需求，歡迎**直接與我本人聯繫**（見[關於我](/about/)頁面的 GitHub / LinkedIn）。

### 設計模式 / 架構
- `gof-design-patterns-java` 🔒 — GoF 設計模式 (Java)
- `gof-design-patterns-cpp` 🔒 — GoF 設計模式 (C++)
- `teddy-dddcleankanban` 🔒 — DDD + Clean Architecture 看板

### Spring / Java 學習
- `spring-framework-6-cert-preparation` 🔒 — Spring Framework 6 認證準備
- `core-spring-labfiles` 🔒 · `spring-boot-labfiles` 🔒 — Spring 官方課程練習
- `Spring_in_Action4` 🔒 — Spring in Action 讀書筆記

### 微服務 / 企業系統
- `ec-microservices` 🔒 — 電商微服務
- `insurance_management_architecture_demo` 🔒 — 保險管理架構示範
- `policy-core-service` 🔒 — 保單核心服務
- `order-app` 🔒 · `microservices-demo` 🔒 — 微服務範例
- `SpringWithKafka` 🔒 — Spring + Kafka
- `Restful-API-client` 🔒 — RESTful API 用戶端

### AI / GraphQL
- `ollama-qdrant-dify-tutorial` 🔒 — Ollama + Qdrant + Dify
- `spring-graphql-example` 🔒 — Spring GraphQL 範例

### 金融 / 銀行領域（客戶／內部專案）
- `banking-benefit-service` 🔒 · `banking-benefit-process-engine-sdd` 🔒 — 銀行權益服務
- `accounting` 🔒 · `account` 🔒 · `position` 🔒 — 會計／帳務／部位
- `aml` 🔒 — 反洗錢 (AML)
- `swift` 🔒 · `correspond-bank-balance` 🔒 · `notification-of-credit` 🔒 · `inward-remittance` 🔒 — 跨行匯兌／清算
- `foundation` 🔒 · `electronicMedia` 🔒 · `flow-mgmt` 🔒 — 共用基礎／流程管理
- `FBPoC202109` 🔒 — 金融業 PoC

### 其他應用
- `stock-folio` 🔒 — 股票投資組合
- `surgeryRecord` 🔒 — 手術紀錄系統
- `azure-spring-cloud-config` 🔒 — Azure Spring Cloud 配置

---

完整清單請參考 [GitHub](https://github.com/ChunPingWang)，或瀏覽部落格的[文章分類](/categories/)。
