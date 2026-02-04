---
layout: single
title: "DevOps 實踐：打造高效 CI/CD Pipeline"
date: 2026-01-31 12:00:00 +0800
categories: [devops]
tags: [devops, cicd, jenkins, github-actions, 自動化]
toc: true
toc_sticky: true
---

DevOps 是開發與運維的融合，CI/CD 則是實現 DevOps 的核心實踐。本文分享如何建立高效的自動化流程。

## CI/CD 基本概念

### 持續整合 (Continuous Integration)

每次程式碼提交都自動建置和測試。

```
程式碼提交 → 自動建置 → 執行測試 → 產生報告
```

### 持續交付 (Continuous Delivery)

自動將通過測試的程式碼部署到預備環境。

### 持續部署 (Continuous Deployment)

自動將程式碼部署到生產環境。

## GitHub Actions 實戰

### 基本 Java 專案 CI

```yaml
# .github/workflows/ci.yml
name: Java CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'

    - name: Cache Gradle packages
      uses: actions/cache@v3
      with:
        path: ~/.gradle/caches
        key: ${{ runner.os }}-gradle-${{ hashFiles('**/*.gradle*') }}

    - name: Build with Gradle
      run: ./gradlew build

    - name: Run tests
      run: ./gradlew test

    - name: Upload test results
      uses: actions/upload-artifact@v3
      if: always()
      with:
        name: test-results
        path: build/reports/tests/
```

### 容器化部署

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4

    - name: Login to Container Registry
      uses: docker/login-action@v3
      with:
        registry: ghcr.io
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}

    - name: Build and push
      uses: docker/build-push-action@v5
      with:
        push: true
        tags: ghcr.io/${{ github.repository }}:${{ github.sha }}

  deploy:
    needs: build-and-push
    runs-on: ubuntu-latest

    steps:
    - name: Deploy to Kubernetes
      uses: azure/k8s-deploy@v4
      with:
        manifests: k8s/
        images: ghcr.io/${{ github.repository }}:${{ github.sha }}
```

## Jenkins Pipeline

### Jenkinsfile 範例

```groovy
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'harbor.example.com'
        APP_NAME = 'my-app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean build -x test'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
            post {
                always {
                    junit 'build/test-results/**/*.xml'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                sh './gradlew sonarqube'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'harbor-credentials') {
                        docker.image("${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}").push()
                        docker.image("${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }

        stage('Deploy to Dev') {
            steps {
                sh "kubectl set image deployment/${APP_NAME} ${APP_NAME}=${DOCKER_REGISTRY}/${APP_NAME}:${BUILD_NUMBER}"
            }
        }
    }

    post {
        success {
            slackSend color: 'good', message: "Build ${BUILD_NUMBER} succeeded!"
        }
        failure {
            slackSend color: 'danger', message: "Build ${BUILD_NUMBER} failed!"
        }
    }
}
```

## 最佳實踐

### 1. 快速回饋

- 測試平行化執行
- 使用快取加速建置
- 失敗時立即通知

### 2. 環境一致性

```dockerfile
# Dockerfile - 確保環境一致
FROM eclipse-temurin:17-jre-alpine
COPY build/libs/app.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### 3. 密鑰管理

```yaml
# 使用 GitHub Secrets
env:
  DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
  API_KEY: ${{ secrets.API_KEY }}
```

### 4. 分支策略

```
main (生產)
  ↑
develop (開發)
  ↑
feature/* (功能分支)
```

## 監控與回滾

### 健康檢查

```yaml
# Kubernetes 健康檢查
livenessProbe:
  httpGet:
    path: /actuator/health
    port: 8080
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /actuator/health/readiness
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

### 快速回滾

```bash
# Kubernetes 回滾
kubectl rollout undo deployment/my-app

# 或回滾到特定版本
kubectl rollout undo deployment/my-app --to-revision=2
```

## 延伸閱讀

- [tap-install-note](https://github.com/ChunPingWang/tap-install-note) - Tanzu Application Platform
- [harbor-install-note](https://github.com/ChunPingWang/harbor-install-note) - Harbor 容器倉庫

自動化一切可以自動化的事情！
