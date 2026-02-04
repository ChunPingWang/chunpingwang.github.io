---
layout: single
title: "GitHub Copilot 工作坊：AI 輔助 Java 開發"
date: 2026-02-04 16:00:00 +0800
categories: [java, ai]
tags: [github-copilot, java, spring-boot, ai, 生產力]
toc: true
toc_sticky: true
---

GitHub Copilot 已經改變了我寫程式的方式。我建立了一個工作坊，教導開發者如何在建構 Java 應用程式時有效運用 Copilot。

## 什麼是 GitHub Copilot？

GitHub Copilot 是一個 AI 程式設計助手，能夠：
- 即時提供程式碼建議
- 從註解生成完整函式
- 協助撰寫測試和文件
- 從你的程式碼庫上下文學習

## 工作坊：TaskList Kata

我們使用 TaskList Kata——一個經典的程式練習——在學習 Copilot 的同時逐步建構任務管理應用程式。

### 從簡單開始

```java
// Copilot 可以從註解生成程式碼：
// 建立一個 Task 類別，包含 id、title 和 completed 狀態
public class Task {
    private Long id;
    private String title;
    private boolean completed;

    // Copilot 會建議建構子、getter、setter
}
```

### 進化到企業級

到課程結束時，你將擁有：
- 多租戶架構
- 帶有 OpenAPI 文件的 REST API
- Spring Security 整合
- 完整的測試覆蓋

## 工作坊模組

### 模組 1：Copilot 基礎
- 了解 Copilot 的運作方式
- 撰寫有效的提示
- 接受、拒絕和修改建議

### 模組 2：CRUD 操作
```java
// 新增任務到清單
public void addTask(String title) {
    // Copilot 建議實作
    Task task = new Task(nextId++, title, false);
    tasks.add(task);
}
```

### 模組 3：測試生成
```java
// Copilot 擅長生成測試
@Test
void shouldAddNewTask() {
    // Given
    TaskList taskList = new TaskList();

    // When
    taskList.addTask("學習 Copilot");

    // Then
    assertEquals(1, taskList.getTasks().size());
}
```

### 模組 4：架構重構
從簡單類別轉換為六角形架構：

```
之前：TaskList.java（單體式）
之後：
├── domain/Task.java
├── application/TaskService.java
├── adapter/TaskController.java
└── port/TaskRepository.java
```

### 模組 5：REST API
```java
@RestController
@RequestMapping("/api/tasks")
public class TaskController {

    @PostMapping
    public ResponseEntity<Task> createTask(@RequestBody CreateTaskRequest request) {
        // Copilot 協助驗證、錯誤處理
    }

    @GetMapping
    public List<Task> getAllTasks() {
        // Copilot 建議分頁、篩選
    }
}
```

### 模組 6：多租戶
SaaS 應用程式的進階模式：
- 租戶隔離策略
- 安全上下文傳播
- 每租戶資料庫 vs 共享 schema

## 有效使用 Copilot 的技巧

1. **撰寫清晰的註解** - Copilot 將其作為提示
2. **使用描述性名稱** - 更好的上下文 = 更好的建議
3. **仔細審查** - AI 可能會犯錯
4. **學習快捷鍵** - 接受、拒絕、切換建議
5. **提供範例** - Copilot 從你程式碼中的模式學習

## 取得工作坊

開始學習：[github-copilot-workshop-java](https://github.com/ChunPingWang/github-copilot-workshop-java)

AI 輔助開發是未來趨勢。學會有效地與 Copilot 合作！
