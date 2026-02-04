---
layout: single
title: "Docker 容器化技術完整指南"
date: 2026-01-30 12:00:00 +0800
categories: [devops, 容器]
tags: [docker, container, 容器化, devops]
toc: true
toc_sticky: true
---

Docker 是容器化技術的代表，讓應用程式能夠在任何環境中一致地運行。本文整理 Docker 的核心概念與實用技巧。

## 容器 vs 虛擬機

| 特性 | 容器 | 虛擬機 |
|------|------|--------|
| 啟動時間 | 秒級 | 分鐘級 |
| 資源佔用 | 輕量 | 較重 |
| 隔離性 | 程序級 | 系統級 |
| 效能 | 接近原生 | 有損耗 |

## Dockerfile 最佳實踐

### 多階段建置 (Multi-stage Build)

```dockerfile
# 建置階段
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn package -DskipTests

# 執行階段
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

# 非 root 使用者
RUN addgroup -g 1001 appgroup && \
    adduser -u 1001 -G appgroup -D appuser
USER appuser

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### 優化層快取

```dockerfile
# 不好的做法 - 每次都重新下載依賴
COPY . /app
RUN npm install

# 好的做法 - 利用快取
COPY package*.json /app/
RUN npm install
COPY . /app
```

### .dockerignore 檔案

```
.git
.gitignore
node_modules
target
*.md
Dockerfile*
docker-compose*
```

## Docker Compose 實戰

### 開發環境配置

```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=dev
      - DB_HOST=db
    depends_on:
      db:
        condition: service_healthy
    volumes:
      - ./src:/app/src  # 開發時熱重載
    networks:
      - app-network

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user -d myapp"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - app-network

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    networks:
      - app-network

volumes:
  postgres-data:

networks:
  app-network:
    driver: bridge
```

### 常用命令

```bash
# 啟動服務
docker-compose up -d

# 查看日誌
docker-compose logs -f app

# 重新建置
docker-compose up -d --build

# 停止並移除
docker-compose down -v
```

## 映像管理

### 標籤策略

```bash
# 語意化版本
docker tag myapp:latest myapp:1.0.0
docker tag myapp:latest myapp:1.0
docker tag myapp:latest myapp:1

# Git commit hash
docker tag myapp:latest myapp:$(git rev-parse --short HEAD)
```

### 映像瘦身

```bash
# 查看映像大小
docker images

# 使用 Alpine 基礎映像
FROM alpine:3.18

# 使用 distroless 映像 (更安全)
FROM gcr.io/distroless/java17-debian11
```

### 安全掃描

```bash
# 使用 Docker Scout
docker scout cves myapp:latest

# 使用 Trivy
trivy image myapp:latest
```

## 網路設定

### 網路類型

```bash
# 建立自訂網路
docker network create --driver bridge my-network

# 連接容器到網路
docker network connect my-network my-container
```

### 容器間通訊

```yaml
# 同一網路內的容器可以用服務名稱互相存取
services:
  web:
    environment:
      - DATABASE_URL=jdbc:postgresql://db:5432/myapp
  db:
    # web 服務可以用 "db" 作為 hostname 連接
```

## 資料持久化

### Volume vs Bind Mount

```yaml
services:
  db:
    volumes:
      # Named volume - Docker 管理
      - postgres-data:/var/lib/postgresql/data

      # Bind mount - 指定路徑
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql

volumes:
  postgres-data:  # 宣告 named volume
```

### Volume 管理

```bash
# 列出所有 volume
docker volume ls

# 清理未使用的 volume
docker volume prune

# 備份 volume
docker run --rm -v postgres-data:/data -v $(pwd):/backup alpine \
  tar czf /backup/postgres-backup.tar.gz /data
```

## 生產環境注意事項

### 資源限制

```yaml
services:
  app:
    deploy:
      resources:
        limits:
          cpus: '2'
          memory: 2G
        reservations:
          cpus: '1'
          memory: 1G
```

### 健康檢查

```dockerfile
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD curl -f http://localhost:8080/actuator/health || exit 1
```

### 日誌管理

```yaml
services:
  app:
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
```

## 延伸閱讀

- [harbor-install-note](https://github.com/ChunPingWang/harbor-install-note) - 私有映像倉庫
- [K8sLabs](https://github.com/ChunPingWang/K8sLabs) - 進階容器編排

容器化是現代應用部署的基礎！
