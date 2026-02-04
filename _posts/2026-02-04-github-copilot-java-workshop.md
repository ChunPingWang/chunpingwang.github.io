---
layout: post
title: "GitHub Copilot Workshop: Building Java Applications with AI"
date: 2026-02-04 16:00:00 +0800
categories: [java, ai]
tags: [github-copilot, java, spring-boot, ai, productivity]
---

GitHub Copilot has transformed how I write code. I've created a workshop that teaches developers how to leverage Copilot effectively while building Java applications.

## What is GitHub Copilot?

GitHub Copilot is an AI pair programmer that:
- Suggests code completions in real-time
- Generates entire functions from comments
- Helps write tests and documentation
- Learns from your codebase context

## The Workshop: TaskList Kata

We use the TaskList Kata - a classic programming exercise - to progressively build a task management application while learning Copilot.

### Starting Simple

```java
// Copilot can generate this from just a comment:
// Create a Task class with id, title, and completed status
public class Task {
    private Long id;
    private String title;
    private boolean completed;

    // Copilot will suggest constructors, getters, setters
}
```

### Evolving to Enterprise-Grade

By the end, you'll have:
- Multi-tenant architecture
- REST API with OpenAPI documentation
- Spring Security integration
- Comprehensive test coverage

## Workshop Modules

### Module 1: Copilot Fundamentals
- Understanding how Copilot works
- Writing effective prompts
- Accepting, rejecting, and modifying suggestions

### Module 2: CRUD Operations
```java
// Add a task to the list
public void addTask(String title) {
    // Copilot suggests the implementation
    Task task = new Task(nextId++, title, false);
    tasks.add(task);
}
```

### Module 3: Test Generation
```java
// Copilot excels at generating tests
@Test
void shouldAddNewTask() {
    // Given
    TaskList taskList = new TaskList();

    // When
    taskList.addTask("Learn Copilot");

    // Then
    assertEquals(1, taskList.getTasks().size());
}
```

### Module 4: Architecture Refactoring
Transform from simple class to hexagonal architecture:

```
Before: TaskList.java (monolithic)
After:
├── domain/Task.java
├── application/TaskService.java
├── adapter/TaskController.java
└── port/TaskRepository.java
```

### Module 5: REST API
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {

    @PostMapping
    public ResponseEntity<Task> createTask(@RequestBody CreateTaskRequest request) {
        // Copilot helps with validation, error handling
    }

    @GetMapping
    public List<Task> getAllTasks() {
        // Copilot suggests pagination, filtering
    }
}
```

### Module 6: Multi-Tenancy
Advanced patterns for SaaS applications:
- Tenant isolation strategies
- Security context propagation
- Database per tenant vs shared schema

## Tips for Effective Copilot Usage

1. **Write clear comments** - Copilot uses them as prompts
2. **Use descriptive names** - Better context = better suggestions
3. **Review carefully** - AI can make mistakes
4. **Learn the shortcuts** - Accept, reject, cycle through suggestions
5. **Provide examples** - Copilot learns from patterns in your code

## Get the Workshop

Start learning: [github-copilot-workshop-java](https://github.com/ChunPingWang/github-copilot-workshop-java)

AI-assisted development is the future. Learn to work with Copilot effectively!
