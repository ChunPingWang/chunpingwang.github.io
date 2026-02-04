---
layout: single
title: "Java 開發最佳實踐與效能優化"
date: 2026-02-04 17:00:00 +0800
categories: [java]
tags: [java, 效能優化, 最佳實踐, jvm]
toc: true
toc_sticky: true
---

Java 是企業級應用開發的主流語言。本文分享一些實用的最佳實踐與效能優化技巧。

## 程式碼品質最佳實踐

### 1. 善用 Optional 避免 NullPointerException

```java
// 不好的寫法
public String getUserName(User user) {
    if (user != null && user.getName() != null) {
        return user.getName();
    }
    return "Unknown";
}

// 好的寫法
public String getUserName(User user) {
    return Optional.ofNullable(user)
            .map(User::getName)
            .orElse("Unknown");
}
```

### 2. 使用 Stream API 簡化集合操作

```java
// 傳統寫法
List<String> activeUserNames = new ArrayList<>();
for (User user : users) {
    if (user.isActive()) {
        activeUserNames.add(user.getName());
    }
}

// Stream 寫法
List<String> activeUserNames = users.stream()
        .filter(User::isActive)
        .map(User::getName)
        .collect(Collectors.toList());
```

### 3. 不可變物件 (Immutable Objects)

```java
public final class User {
    private final String name;
    private final String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() { return name; }
    public String getEmail() { return email; }
}
```

## 效能優化技巧

### 1. 字串串接使用 StringBuilder

```java
// 不好的寫法 - 每次串接都產生新物件
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;
}

// 好的寫法
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);
}
String result = sb.toString();
```

### 2. 選擇適當的集合類型

| 場景 | 推薦類型 |
|------|----------|
| 頻繁隨機存取 | ArrayList |
| 頻繁插入刪除 | LinkedList |
| 需要唯一性 | HashSet |
| 需要排序 | TreeSet |
| Key-Value 對應 | HashMap |
| 需要排序的 Map | TreeMap |

### 3. 使用連接池

```java
// HikariCP 設定範例
HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/mydb");
config.setUsername("user");
config.setPassword("password");
config.setMaximumPoolSize(10);
config.setMinimumIdle(5);

HikariDataSource dataSource = new HikariDataSource(config);
```

## JVM 調優基礎

### 常用 JVM 參數

```bash
# 設定堆記憶體
java -Xms512m -Xmx2g -jar app.jar

# 設定垃圾回收器
java -XX:+UseG1GC -jar app.jar

# 啟用 GC 日誌
java -Xlog:gc*:file=gc.log -jar app.jar
```

### 記憶體洩漏排查

```bash
# 產生 heap dump
jmap -dump:format=b,file=heap.hprof <pid>

# 使用 jstat 監控 GC
jstat -gc <pid> 1000
```

## 延伸閱讀

- [Effective Java](https://www.oreilly.com/library/view/effective-java/9780134686097/) - Joshua Bloch
- [Java Performance](https://www.oreilly.com/library/view/java-performance-2nd/9781492056102/) - Scott Oaks

持續學習，寫出更好的 Java 程式碼！
