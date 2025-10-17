---
title: "Hiểu về Java Virtual Machine (JVM)"
date: 2025-10-17
category: "Java"
image: "images/javajvm.jpg"
description: "Java Virtual Machine (JVM) là trái tim của nền tảng Java. Tìm hiểu kiến trúc JVM bao gồm Class Loader, Runtime Data Areas, Execution Engine, và cơ chế Garbage Collection để quản lý bộ nhớ tự động."
---

Java Virtual Machine (JVM) là trái tim của nền tảng Java, đóng vai trò quan trọng trong việc thực thi các chương trình Java.

## JVM là gì?

JVM là một máy ảo cho phép máy tính chạy các chương trình Java cũng như các chương trình được viết bằng các ngôn ngữ khác được biên dịch thành Java bytecode.

## Kiến trúc của JVM

JVM bao gồm ba thành phần chính:

### Class Loader

Class Loader chịu trách nhiệm:
- Tải các class file vào bộ nhớ
- Linking (liên kết các class với nhau)
- Initialization (khởi tạo biến static)

### Runtime Data Areas

Các vùng nhớ mà JVM sử dụng:

**Method Area**: Lưu trữ thông tin về class, method, field

**Heap**: Vùng nhớ chính để lưu trữ objects và arrays

**Stack**: Mỗi thread có một stack riêng, lưu local variables và method calls

**PC Register**: Lưu địa chỉ của instruction đang thực thi

**Native Method Stack**: Cho các native methods (C/C++)

### Execution Engine

Thực thi bytecode thông qua:
- Interpreter: Đọc và thực thi bytecode từng dòng
- JIT Compiler: Biên dịch bytecode thành native code để tăng hiệu suất
- Garbage Collector: Tự động thu hồi bộ nhớ

## Quá trình thực thi Java Program

1. Viết source code (.java file)
2. Compiler biên dịch thành bytecode (.class file)
3. Class Loader tải bytecode vào JVM
4. Bytecode Verifier kiểm tra tính hợp lệ
5. Execution Engine thực thi bytecode

## Garbage Collection

Garbage Collector (GC) tự động quản lý bộ nhớ bằng cách:
- Xác định objects không còn được tham chiếu
- Thu hồi bộ nhớ của các objects đó
- Giải phóng không gian cho objects mới

### Các thuật toán GC phổ biến:
- Serial GC
- Parallel GC
- CMS (Concurrent Mark Sweep)
- G1GC (Garbage First)
- ZGC (Z Garbage Collector)

## JVM vs JRE vs JDK

**JVM**: Máy ảo thực thi bytecode

**JRE (Java Runtime Environment)**: JVM + thư viện chuẩn để chạy Java applications

**JDK (Java Development Kit)**: JRE + các công cụ phát triển (compiler, debugger, etc.)

## Lợi ích của JVM

- Độc lập nền tảng
- Quản lý bộ nhớ tự động
- Bảo mật cao thông qua bytecode verification
- Tối ưu hóa hiệu suất với JIT compiler
- Hỗ trợ đa ngôn ngữ (Kotlin, Scala, Groovy)

Hiểu rõ về JVM giúp developers viết code hiệu quả hơn và debug các vấn đề về hiệu suất.