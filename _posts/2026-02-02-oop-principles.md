---
layout: single
title: "物件導向設計原則與 SOLID 實踐"
date: 2026-02-02 12:00:00 +0800
categories: [java, oop]
tags: [oop, solid, 物件導向, 設計原則]
toc: true
toc_sticky: true
---

物件導向程式設計 (OOP) 是現代軟體開發的基石。掌握 SOLID 原則能幫助你寫出更易維護、更具彈性的程式碼。

## OOP 四大特性

### 1. 封裝 (Encapsulation)

隱藏內部實作細節，只暴露必要的介面。

```java
public class BankAccount {
    private double balance;  // 隱藏內部狀態

    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            this.balance -= amount;
            return true;
        }
        return false;
    }

    public double getBalance() {
        return balance;  // 只讀存取
    }
}
```

### 2. 繼承 (Inheritance)

建立類別之間的「是一種」(is-a) 關係。

```java
public abstract class Shape {
    protected String color;

    public abstract double area();
}

public class Circle extends Shape {
    private double radius;

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```

### 3. 多型 (Polymorphism)

同一介面，不同實作。

```java
public interface PaymentProcessor {
    void process(Payment payment);
}

public class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void process(Payment payment) {
        // 信用卡處理邏輯
    }
}

public class PayPalProcessor implements PaymentProcessor {
    @Override
    public void process(Payment payment) {
        // PayPal 處理邏輯
    }
}

// 使用時
PaymentProcessor processor = getProcessor(paymentType);
processor.process(payment);  // 多型呼叫
```

### 4. 抽象 (Abstraction)

專注於「做什麼」而非「怎麼做」。

```java
public interface EmailService {
    void send(String to, String subject, String body);
}
// 使用者不需要知道郵件是透過 SMTP、API 還是其他方式發送
```

## SOLID 原則

### S - 單一職責原則 (Single Responsibility)

一個類別應該只有一個改變的理由。

```java
// 不好的設計 - 一個類別做太多事
public class User {
    public void saveToDatabase() { }
    public void sendEmail() { }
    public String generateReport() { }
}

// 好的設計 - 職責分離
public class User { }
public class UserRepository {
    public void save(User user) { }
}
public class UserNotificationService {
    public void sendWelcomeEmail(User user) { }
}
```

### O - 開放封閉原則 (Open/Closed)

對擴展開放，對修改封閉。

```java
// 使用策略模式實現
public interface DiscountStrategy {
    double calculate(double price);
}

public class RegularDiscount implements DiscountStrategy {
    public double calculate(double price) {
        return price * 0.1;
    }
}

public class VIPDiscount implements DiscountStrategy {
    public double calculate(double price) {
        return price * 0.2;
    }
}

// 新增折扣類型時，不需修改現有程式碼
public class HolidayDiscount implements DiscountStrategy {
    public double calculate(double price) {
        return price * 0.3;
    }
}
```

### L - 里氏替換原則 (Liskov Substitution)

子類別應該可以替換父類別而不影響程式正確性。

```java
// 違反 LSP 的經典例子
public class Rectangle {
    protected int width, height;

    public void setWidth(int w) { width = w; }
    public void setHeight(int h) { height = h; }
    public int area() { return width * height; }
}

public class Square extends Rectangle {
    @Override
    public void setWidth(int w) {
        width = height = w;  // 違反 LSP！
    }
}

// 更好的設計
public interface Shape {
    int area();
}
public class Rectangle implements Shape { }
public class Square implements Shape { }
```

### I - 介面隔離原則 (Interface Segregation)

不應強迫客戶端依賴它不使用的方法。

```java
// 不好的設計 - 胖介面
public interface Worker {
    void work();
    void eat();
    void sleep();
}

// 好的設計 - 細粒度介面
public interface Workable {
    void work();
}

public interface Eatable {
    void eat();
}

public class Human implements Workable, Eatable {
    public void work() { }
    public void eat() { }
}

public class Robot implements Workable {
    public void work() { }
    // 機器人不需要吃東西
}
```

### D - 依賴反轉原則 (Dependency Inversion)

高層模組不應依賴低層模組，兩者都應依賴抽象。

```java
// 不好的設計 - 直接依賴具體實作
public class OrderService {
    private MySQLDatabase database = new MySQLDatabase();
}

// 好的設計 - 依賴抽象
public class OrderService {
    private final OrderRepository repository;

    public OrderService(OrderRepository repository) {
        this.repository = repository;  // 注入抽象
    }
}

public interface OrderRepository {
    void save(Order order);
}

public class MySQLOrderRepository implements OrderRepository { }
public class MongoOrderRepository implements OrderRepository { }
```

## 實踐建議

1. **優先使用組合而非繼承** - 組合更靈活
2. **針對介面程式設計** - 降低耦合度
3. **保持類別小而專注** - 容易測試和維護
4. **及早重構** - 發現壞味道立即處理

## 延伸閱讀

- Clean Code - Robert C. Martin
- Refactoring - Martin Fowler
- Head First Design Patterns

SOLID 原則是寫出高品質程式碼的基礎！
