---
title: "Lập trình hướng đối tượng (OOP) trong Java"
date: 2025-10-18
category: "Java"
image: "images/javaoop.jpg"
description: "Lập trình hướng đối tượng (OOP) là nền tảng của Java. Nắm vững 4 nguyên lý cơ bản: Encapsulation (Đóng gói), Inheritance (Kế thừa), Polymorphism (Đa hình), và Abstraction (Trừu tượng) với ví dụ thực tế."
---

Lập trình hướng đối tượng (Object-Oriented Programming - OOP) là paradigm lập trình quan trọng nhất trong Java.

## 4 Nguyên lý cơ bản của OOP

### 1. Encapsulation (Đóng gói)

Encapsulation là việc ẩn giấu dữ liệu và chỉ cho phép truy cập thông qua các methods.

```java
public class BankAccount {
    private double balance; // private - ẩn giấu dữ liệu
    
    public double getBalance() {
        return balance;
    }
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
}
```

**Lợi ích**: Bảo vệ dữ liệu, dễ bảo trì, tăng tính linh hoạt

### 2. Inheritance (Kế thừa)

Cho phép class con kế thừa thuộc tính và methods từ class cha.

```java
public class Animal {
    protected String name;
    
    public void eat() {
        System.out.println("Đang ăn...");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("Gâu gâu!");
    }
}
```

**Lợi ích**: Tái sử dụng code, tạo cấu trúc phân cấp

### 3. Polymorphism (Đa hình)

Một object có thể có nhiều hình thái khác nhau.

**Method Overloading** (Compile-time polymorphism):

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}
```

**Method Overriding** (Runtime polymorphism):

```java
public class Animal {
    public void makeSound() {
        System.out.println("Some sound");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}
```

**Lợi ích**: Code linh hoạt, dễ mở rộng

### 4. Abstraction (Trừu tượng)

Ẩn giấu chi tiết implementation, chỉ hiển thị chức năng cần thiết.

**Abstract Class**:

```java
public abstract class Shape {
    abstract double calculateArea();
    
    public void display() {
        System.out.println("Area: " + calculateArea());
    }
}

public class Circle extends Shape {
    private double radius;
    
    @Override
    double calculateArea() {
        return Math.PI * radius * radius;
    }
}
```

**Interface**:

```java
public interface Drawable {
    void draw();
}

public class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
}
```

## Class và Object

**Class** là blueprint (bản thiết kế) để tạo objects.

**Object** là instance của class.

```java
public class Car {
    String brand;
    String model;
    int year;
    
    public void start() {
        System.out.println("Car is starting");
    }
}

// Tạo object
Car myCar = new Car();
myCar.brand = "Toyota";
myCar.start();
```

## Constructor

Constructor là method đặc biệt được gọi khi tạo object.

```java
public class Person {
    private String name;
    private int age;
    
    // Default constructor
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    // Parameterized constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

## Access Modifiers

- **private**: Chỉ truy cập trong class
- **default**: Truy cập trong package
- **protected**: Truy cập trong package và subclasses
- **public**: Truy cập mọi nơi

OOP giúp code có cấu trúc tốt hơn, dễ bảo trì và mở rộng, đây là nền tảng quan trọng để trở thành Java developer giỏi.