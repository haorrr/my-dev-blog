---
title: "Lập trình hướng đối tượng (OOP) trong Java"
date: 2025-10-18
category: "Java"
image: "/images/javaoop.jpg"
description: "Lập trình hướng đối tượng (OOP) là nền tảng của Java. Nắm vững 4 nguyên lý cơ bản: Encapsulation (Đóng gói), Inheritance (Kế thừa), Polymorphism (Đa hình), và Abstraction (Trừu tượng) với ví dụ thực tế."
---

Lập trình hướng đối tượng (Object-Oriented Programming - OOP) là linh hồn của ngôn ngữ Java.  
Nhờ có OOP, Java giúp việc phát triển phần mềm trở nên có tổ chức, dễ mở rộng và gần gũi hơn với cách con người mô hình hóa thế giới thực.  
Trong bài viết này, chúng ta sẽ tìm hiểu 4 nguyên lý cơ bản của OOP trong Java cùng với ví dụ cụ thể.

---

## 1. Khái niệm lập trình hướng đối tượng

OOP là phương pháp lập trình tổ chức chương trình dựa trên **đối tượng (object)** – những thực thể có dữ liệu (thuộc tính) và hành vi (phương thức).  
Thay vì viết toàn bộ code trong các hàm rời rạc, Java cho phép ta nhóm logic liên quan lại với nhau thành các class – giúp chương trình rõ ràng, dễ bảo trì và tái sử dụng.

---

## 2. Các nguyên lý cơ bản của OOP trong Java

### 2.1. Encapsulation – Đóng gói

Đóng gói nghĩa là ẩn giấu dữ liệu bên trong đối tượng và chỉ cho phép truy cập thông qua các phương thức công khai.  
Cách làm này giúp bảo vệ dữ liệu khỏi bị thay đổi trực tiếp, đồng thời đảm bảo tính an toàn và toàn vẹn của đối tượng.

Ví dụ:

```java
public class BankAccount {
    private double balance; // không thể truy cập trực tiếp từ bên ngoài

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
Trong ví dụ trên, biến balance được ẩn đi bằng từ khóa private, và chỉ được truy cập thông qua các phương thức getBalance() và deposit().

### 2.2. Inheritance – Kế thừa
Kế thừa cho phép một class con tái sử dụng lại thuộc tính và phương thức của class cha.
Điều này giúp giảm lặp code và cho phép mở rộng chức năng dễ dàng.

Ví dụ:

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
Class Dog kế thừa từ Animal, nhờ đó có thể sử dụng lại phương thức eat() mà không cần viết lại.

### 2.3. Polymorphism – Đa hình
Đa hình cho phép cùng một hành động có thể có nhiều cách thực hiện khác nhau tùy theo đối tượng cụ thể.
Trong Java, đa hình thể hiện qua method overloading (đa hình khi biên dịch) và method overriding (đa hình khi chạy).

Ví dụ về Overloading:

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
Ví dụ về Overriding:

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
Cả Cat và Animal đều có makeSound(), nhưng hành vi của mỗi class lại khác nhau – minh chứng cho tính đa hình.

### 2.4. Abstraction – Trừu tượng
Trừu tượng giúp che giấu chi tiết triển khai phức tạp, chỉ để lộ phần cần thiết cho người dùng. hỗ trợ trừu tượng thông qua abstract class và interface.

Ví dụ với abstract class:

public abstract class Shape {
    abstract double calculateArea();

    public void display() {
        System.out.println("Area: " + calculateArea());
    }
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double calculateArea() {
        return Math.PI * radius * radius;
    }
}
Ví dụ với interface:


public interface Drawable {
    void draw();
}

public class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
}
Nhờ cơ chế trừu tượng, ta có thể dễ dàng mở rộng chương trình mà không cần sửa đổi lớp hiện có.

## 3. Class, Object và Constructor
### 3.1. Class và Object
Class là bản thiết kế (blueprint) cho các đối tượng.

Object là thể hiện (instance) của class.

Ví dụ:


public class Car {
    String brand;
    int year;

    public void start() {
        System.out.println("Car is starting");
    }
}

Car myCar = new Car();
myCar.brand = "Toyota";
myCar.start();
### 3.2. Constructor
Là phương thức đặc biệt được gọi khi tạo đối tượng.
Constructor có thể có tham số hoặc không.


public class Person {
    private String name;
    private int age;

    // Constructor mặc định
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }

    // Constructor có tham số
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}


## 4. Kết luận
Lập trình hướng đối tượng là nền tảng giúp Java mạnh mẽ, dễ mở rộng và bảo trì.
Nắm vững bốn nguyên lý Encapsulation, Inheritance, Polymorphism và Abstraction không chỉ giúp bạn viết code tốt hơn, mà còn hình thành tư duy lập trình chuyên nghiệp.
Khi bạn hiểu OOP, bạn đã nắm được “linh hồn” của Java và sẵn sàng bước vào các khái niệm nâng cao hơn như thiết kế mô hình, framework và cấu trúc phần mềm thực tế.