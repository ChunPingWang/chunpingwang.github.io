---
layout: single
title: "Spring Boot 核心概念與實戰技巧"
date: 2026-02-03 12:00:00 +0800
categories: [java, spring]
tags: [spring-boot, spring, 微服務, java]
toc: true
toc_sticky: true
---

Spring Boot 大幅簡化了 Spring 應用程式的開發。本文整理核心概念與常用技巧。

## Spring Boot 自動配置

Spring Boot 的魔力來自於自動配置 (Auto-configuration)。當你加入相關依賴時，Spring Boot 會自動配置對應的元件。

### 原理解析

```java
@SpringBootApplication
// 等同於
@SpringBootConfiguration
@EnableAutoConfiguration  // 關鍵！啟用自動配置
@ComponentScan
```

### 查看自動配置報告

```bash
java -jar app.jar --debug
# 或在 application.properties
debug=true
```

## 常用註解整理

### 元件相關

| 註解 | 用途 |
|------|------|
| `@Component` | 通用元件 |
| `@Service` | 業務邏輯層 |
| `@Repository` | 資料存取層 |
| `@Controller` | Web 控制器 |
| `@RestController` | REST API 控制器 |

### 依賴注入

```java
// 建構子注入 (推薦)
@Service
public class UserService {
    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}

// 或使用 Lombok
@Service
@RequiredArgsConstructor
public class UserService {
    private final UserRepository repository;
}
```

## 設定檔管理

### application.yml 結構

```yaml
spring:
  application:
    name: my-service
  profiles:
    active: dev
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: ${DB_USERNAME:root}
    password: ${DB_PASSWORD:password}

server:
  port: 8080

# 自訂設定
app:
  feature:
    enabled: true
    max-items: 100
```

### 讀取自訂設定

```java
@Configuration
@ConfigurationProperties(prefix = "app.feature")
@Data
public class FeatureProperties {
    private boolean enabled;
    private int maxItems;
}
```

## REST API 開發

### 控制器範例

```java
@RestController
@RequestMapping("/api/users")
@RequiredArgsConstructor
public class UserController {

    private final UserService userService;

    @GetMapping
    public List<UserDto> findAll() {
        return userService.findAll();
    }

    @GetMapping("/{id}")
    public ResponseEntity<UserDto> findById(@PathVariable Long id) {
        return userService.findById(id)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public UserDto create(@Valid @RequestBody CreateUserRequest request) {
        return userService.create(request);
    }

    @DeleteMapping("/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void delete(@PathVariable Long id) {
        userService.delete(id);
    }
}
```

### 全域例外處理

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EntityNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ErrorResponse handleNotFound(EntityNotFoundException ex) {
        return new ErrorResponse("NOT_FOUND", ex.getMessage());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public ErrorResponse handleValidation(MethodArgumentNotValidException ex) {
        String message = ex.getBindingResult().getFieldErrors().stream()
                .map(e -> e.getField() + ": " + e.getDefaultMessage())
                .collect(Collectors.joining(", "));
        return new ErrorResponse("VALIDATION_ERROR", message);
    }
}
```

## Spring Data JPA

### Repository 介面

```java
public interface UserRepository extends JpaRepository<User, Long> {

    Optional<User> findByEmail(String email);

    List<User> findByActiveTrue();

    @Query("SELECT u FROM User u WHERE u.createdAt > :date")
    List<User> findRecentUsers(@Param("date") LocalDateTime date);
}
```

### 審計功能

```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @CreatedDate
    private LocalDateTime createdAt;

    @LastModifiedDate
    private LocalDateTime updatedAt;
}
```

## Actuator 監控

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: when_authorized
```

常用端點：
- `/actuator/health` - 健康檢查
- `/actuator/info` - 應用資訊
- `/actuator/metrics` - 指標數據

## 延伸閱讀

查看我的 Spring 相關專案：
- [clean_architecture_with_Spring](https://github.com/ChunPingWang/clean_architecture_with_Spring)
- [github-copilot-workshop-java](https://github.com/ChunPingWang/github-copilot-workshop-java)

Spring Boot 讓 Java 開發變得更加高效！
