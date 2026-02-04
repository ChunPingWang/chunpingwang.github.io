---
layout: single
title: "常用設計模式與實戰應用"
date: 2026-02-01 12:00:00 +0800
categories: [java, 設計模式]
tags: [design-pattern, 設計模式, java, 架構]
toc: true
toc_sticky: true
---

設計模式是前人智慧的結晶，是解決常見問題的經典方案。本文介紹幾個最實用的設計模式。

## 創建型模式

### 單例模式 (Singleton)

確保一個類別只有一個實例。

```java
// 推薦：使用 enum 實現
public enum DatabaseConnection {
    INSTANCE;

    private Connection connection;

    public Connection getConnection() {
        if (connection == null) {
            connection = createConnection();
        }
        return connection;
    }
}

// 使用
Connection conn = DatabaseConnection.INSTANCE.getConnection();
```

### 工廠模式 (Factory)

將物件創建邏輯封裝起來。

```java
public interface Notification {
    void send(String message);
}

public class EmailNotification implements Notification {
    public void send(String message) {
        System.out.println("發送 Email: " + message);
    }
}

public class SMSNotification implements Notification {
    public void send(String message) {
        System.out.println("發送簡訊: " + message);
    }
}

public class NotificationFactory {
    public static Notification create(String type) {
        return switch (type) {
            case "email" -> new EmailNotification();
            case "sms" -> new SMSNotification();
            default -> throw new IllegalArgumentException("未知類型: " + type);
        };
    }
}

// 使用
Notification notification = NotificationFactory.create("email");
notification.send("Hello!");
```

### 建造者模式 (Builder)

分步驟建構複雜物件。

```java
public class HttpRequest {
    private final String url;
    private final String method;
    private final Map<String, String> headers;
    private final String body;

    private HttpRequest(Builder builder) {
        this.url = builder.url;
        this.method = builder.method;
        this.headers = builder.headers;
        this.body = builder.body;
    }

    public static class Builder {
        private String url;
        private String method = "GET";
        private Map<String, String> headers = new HashMap<>();
        private String body;

        public Builder url(String url) {
            this.url = url;
            return this;
        }

        public Builder method(String method) {
            this.method = method;
            return this;
        }

        public Builder header(String key, String value) {
            this.headers.put(key, value);
            return this;
        }

        public Builder body(String body) {
            this.body = body;
            return this;
        }

        public HttpRequest build() {
            return new HttpRequest(this);
        }
    }
}

// 使用
HttpRequest request = new HttpRequest.Builder()
        .url("https://api.example.com/users")
        .method("POST")
        .header("Content-Type", "application/json")
        .body("{\"name\": \"Rex\"}")
        .build();
```

## 結構型模式

### 轉接器模式 (Adapter)

讓不相容的介面能夠合作。

```java
// 舊系統的介面
public class LegacyPaymentSystem {
    public void processPayment(String cardNumber, double amount) {
        // 舊的支付邏輯
    }
}

// 新系統期望的介面
public interface PaymentGateway {
    void pay(PaymentRequest request);
}

// 轉接器
public class LegacyPaymentAdapter implements PaymentGateway {
    private final LegacyPaymentSystem legacy;

    public LegacyPaymentAdapter(LegacyPaymentSystem legacy) {
        this.legacy = legacy;
    }

    @Override
    public void pay(PaymentRequest request) {
        legacy.processPayment(
            request.getCardNumber(),
            request.getAmount()
        );
    }
}
```

### 裝飾者模式 (Decorator)

動態地為物件添加功能。

```java
public interface Coffee {
    double cost();
    String description();
}

public class Espresso implements Coffee {
    public double cost() { return 50; }
    public String description() { return "濃縮咖啡"; }
}

public abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
}

public class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    public double cost() {
        return coffee.cost() + 15;
    }

    public String description() {
        return coffee.description() + " + 牛奶";
    }
}

// 使用
Coffee latte = new MilkDecorator(new Espresso());
System.out.println(latte.description());  // 濃縮咖啡 + 牛奶
System.out.println(latte.cost());         // 65
```

## 行為型模式

### 策略模式 (Strategy)

定義一系列演算法，讓它們可以互換。

```java
public interface SortStrategy {
    void sort(int[] array);
}

public class QuickSort implements SortStrategy {
    public void sort(int[] array) {
        // 快速排序實作
    }
}

public class MergeSort implements SortStrategy {
    public void sort(int[] array) {
        // 合併排序實作
    }
}

public class Sorter {
    private SortStrategy strategy;

    public void setStrategy(SortStrategy strategy) {
        this.strategy = strategy;
    }

    public void sort(int[] array) {
        strategy.sort(array);
    }
}

// 使用 - 可動態切換演算法
Sorter sorter = new Sorter();
sorter.setStrategy(new QuickSort());
sorter.sort(data);
```

### 觀察者模式 (Observer)

定義一對多的依賴關係。

```java
public interface Observer {
    void update(String event);
}

public class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String event) {
        for (Observer observer : observers) {
            observer.update(event);
        }
    }
}

// 使用
Subject stockPrice = new Subject();
stockPrice.addObserver(event -> System.out.println("Email 通知: " + event));
stockPrice.addObserver(event -> System.out.println("App 推播: " + event));
stockPrice.notifyObservers("股價上漲 5%");
```

### 模板方法模式 (Template Method)

定義演算法骨架，讓子類別實作細節。

```java
public abstract class DataProcessor {
    // 模板方法 - 定義流程
    public final void process() {
        readData();
        processData();
        writeData();
    }

    protected abstract void readData();
    protected abstract void processData();
    protected abstract void writeData();
}

public class CSVProcessor extends DataProcessor {
    protected void readData() {
        System.out.println("讀取 CSV 檔案");
    }

    protected void processData() {
        System.out.println("處理資料");
    }

    protected void writeData() {
        System.out.println("輸出結果");
    }
}
```

## 設計模式選擇指南

| 問題 | 推薦模式 |
|------|----------|
| 需要唯一實例 | Singleton |
| 建構複雜物件 | Builder |
| 隱藏物件創建 | Factory |
| 介面不相容 | Adapter |
| 動態添加功能 | Decorator |
| 演算法可切換 | Strategy |
| 事件通知 | Observer |
| 固定流程步驟 | Template Method |

## 延伸閱讀

- [clean_architecture_with_Spring](https://github.com/ChunPingWang/clean_architecture_with_Spring)

設計模式是工具，不是目的。根據實際需求選擇合適的模式！
