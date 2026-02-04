---
layout: single
title: "使用 Spring Boot 實作 Clean Architecture"
date: 2026-02-04 14:00:00 +0800
categories: [java, 架構]
tags: [clean-architecture, spring-boot, java, 設計模式, hexagonal]
toc: true
toc_sticky: true
---

Clean Architecture 由 Robert C. Martin（Uncle Bob）提出，幫助我們建立獨立於框架、可測試且易於維護的系統。以下是我在 Spring Boot 中實作的方式。

## 為什麼需要 Clean Architecture？

傳統的分層架構常導致：
- 業務邏輯與框架緊密耦合
- 難以在沒有基礎設施的情況下測試
- 以資料庫為中心而非領域為中心的設計

Clean Architecture 透過強制執行**依賴規則**來解決這些問題——外層依賴內層，反過來則不行。

## 架構分層

```
┌─────────────────────────────────────────┐
│           框架與驅動程式                 │  ← Controllers, DB, Web
├─────────────────────────────────────────┤
│           介面轉接器                     │  ← Presenters, Gateways
├─────────────────────────────────────────┤
│           應用程式業務                   │  ← Use Cases
├─────────────────────────────────────────┤
│           企業業務                       │  ← Entities, Domain
└─────────────────────────────────────────┘
```

## 專案結構

```
src/main/java/com/example/
├── domain/                    # 企業業務規則
│   ├── entity/
│   │   └── Task.java
│   └── repository/
│       └── TaskRepository.java  # 僅介面
├── application/               # 應用程式業務規則
│   ├── usecase/
│   │   ├── CreateTaskUseCase.java
│   │   └── GetTaskUseCase.java
│   └── port/
│       ├── in/               # 輸入埠
│       └── out/              # 輸出埠
├── adapter/                   # 介面轉接器
│   ├── in/
│   │   └── web/
│   │       └── TaskController.java
│   └── out/
│       └── persistence/
│           ├── TaskJpaRepository.java
│           └── TaskPersistenceAdapter.java
└── infrastructure/            # 框架與驅動程式
    └── config/
        └── BeanConfig.java
```

## 領域實體

```java
// 領域層 - 不依賴任何框架
public class Task {
    private Long id;
    private String title;
    private boolean completed;

    public void complete() {
        this.completed = true;
    }

    // 業務規則放這裡
}
```

## 使用案例

```java
// 應用程式層
public class CreateTaskUseCase {
    private final TaskRepository repository;

    public CreateTaskUseCase(TaskRepository repository) {
        this.repository = repository;
    }

    public Task execute(String title) {
        Task task = new Task(title);
        return repository.save(task);
    }
}
```

## Repository 介面（Port）

```java
// 領域層 - 僅定義介面
public interface TaskRepository {
    Task save(Task task);
    Optional<Task> findById(Long id);
    List<Task> findAll();
}
```

## 持久化轉接器

```java
// 轉接器層 - 實作 port
@Component
public class TaskPersistenceAdapter implements TaskRepository {
    private final TaskJpaRepository jpaRepository;

    @Override
    public Task save(Task task) {
        TaskEntity entity = toEntity(task);
        return toDomain(jpaRepository.save(entity));
    }
}
```

## 優點

1. **可測試性** - 無需 Spring 容器即可測試 Use Case
2. **彈性** - 輕鬆替換資料庫或框架
3. **可維護性** - 明確的邊界與職責
4. **專注度** - 業務邏輯獨立且清晰

## 專案連結

探索我的實作：[clean_architecture_with_Spring](https://github.com/ChunPingWang/clean_architecture_with_Spring)

Clean Architecture 需要更多前期規劃，但在長期維護上會帶來豐厚回報。
