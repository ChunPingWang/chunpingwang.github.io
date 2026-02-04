---
layout: post
title: "Implementing Clean Architecture with Spring Boot"
date: 2026-02-04 14:00:00 +0800
categories: [java, architecture]
tags: [clean-architecture, spring-boot, java, design-patterns, hexagonal]
---

Clean Architecture, popularized by Robert C. Martin (Uncle Bob), helps create systems that are independent of frameworks, testable, and maintainable. Here's how I implement it with Spring Boot.

## Why Clean Architecture?

Traditional layered architecture often leads to:
- Tight coupling between business logic and frameworks
- Difficulty testing without infrastructure
- Database-driven design instead of domain-driven

Clean Architecture solves these by enforcing **dependency rules** - outer layers depend on inner layers, never the reverse.

## The Layers

```
┌─────────────────────────────────────────┐
│           Frameworks & Drivers          │  ← Controllers, DB, Web
├─────────────────────────────────────────┤
│          Interface Adapters             │  ← Presenters, Gateways
├─────────────────────────────────────────┤
│           Application Business          │  ← Use Cases
├─────────────────────────────────────────┤
│          Enterprise Business            │  ← Entities, Domain
└─────────────────────────────────────────┘
```

## Project Structure

```
src/main/java/com/example/
├── domain/                    # Enterprise Business Rules
│   ├── entity/
│   │   └── Task.java
│   └── repository/
│       └── TaskRepository.java  # Interface only
├── application/               # Application Business Rules
│   ├── usecase/
│   │   ├── CreateTaskUseCase.java
│   │   └── GetTaskUseCase.java
│   └── port/
│       ├── in/               # Input ports
│       └── out/              # Output ports
├── adapter/                   # Interface Adapters
│   ├── in/
│   │   └── web/
│   │       └── TaskController.java
│   └── out/
│       └── persistence/
│           ├── TaskJpaRepository.java
│           └── TaskPersistenceAdapter.java
└── infrastructure/            # Frameworks & Drivers
    └── config/
        └── BeanConfig.java
```

## Domain Entity

```java
// Domain layer - no framework dependencies
public class Task {
    private Long id;
    private String title;
    private boolean completed;

    public void complete() {
        this.completed = true;
    }

    // Business rules here
}
```

## Use Case

```java
// Application layer
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

## Repository Interface (Port)

```java
// Domain layer - interface only
public interface TaskRepository {
    Task save(Task task);
    Optional<Task> findById(Long id);
    List<Task> findAll();
}
```

## Persistence Adapter

```java
// Adapter layer - implements the port
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

## Benefits

1. **Testability** - Test use cases without Spring context
2. **Flexibility** - Swap databases or frameworks easily
3. **Maintainability** - Clear boundaries and responsibilities
4. **Focus** - Business logic is isolated and clear

## Project Repository

Explore my implementation: [clean_architecture_with_Spring](https://github.com/ChunPingWang/clean_architecture_with_Spring)

Clean Architecture requires more upfront structure, but pays dividends in long-term maintainability.
