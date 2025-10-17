---
title: "JavaScript là gì? Khởi đầu với ngôn ngữ web phổ biến nhất"
date: 2025-10-12
category: "JavaScript"
image: "/images/jsgioithieu.jpg"
description: "JavaScript là ngôn ngữ lập trình phổ biến nhất thế giới, trụ cột của web development. Tìm hiểu cú pháp cơ bản, đặc điểm dynamically typed, first-class functions và ứng dụng từ client-side đến server-side với Node.js."
---

JavaScript là ngôn ngữ lập trình được sử dụng nhiều nhất trên thế giới, là trụ cột của web development hiện đại.

## JavaScript là gì?

JavaScript là ngôn ngữ lập trình high-level, interpreted, được thiết kế để tạo tính tương tác cho trang web. Ban đầu chỉ chạy trên browser, giờ đây JavaScript có thể chạy ở mọi nơi nhờ Node.js.

## Đặc điểm của JavaScript

### Interpreted Language

JavaScript được thực thi trực tiếp bởi trình duyệt hoặc runtime environment mà không cần biên dịch trước.

### Dynamically Typed

Không cần khai báo kiểu dữ liệu cho biến:

```javascript
let message = "Hello"; // string
message = 42; // Có thể thay đổi thành number
message = true; // hoặc boolean
```

### Prototype-based OOP

JavaScript sử dụng prototypes thay vì classes truyền thống (mặc dù ES6 đã có class syntax sugar).

### First-class Functions

Functions là objects, có thể gán cho biến, truyền làm arguments:

```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};

function executeFunction(func, value) {
    return func(value);
}

executeFunction(greet, "John"); // "Hello, John!"
```

## Cú pháp cơ bản

### Variables

```javascript
// var - function scope (tránh dùng)
var oldWay = "old";

// let - block scope, có thể thay đổi
let count = 0;
count = 1;

// const - block scope, không thể thay đổi
const PI = 3.14159;
```

### Data Types

```javascript
// Primitive types
let str = "Hello";          // String
let num = 42;               // Number
let bool = true;            // Boolean
let nothing = null;         // Null
let notDefined;             // Undefined
let sym = Symbol("id");     // Symbol
let big = 9007199254740991n; // BigInt

// Object types
let obj = { name: "John" };
let arr = [1, 2, 3];
let func = function() {};
```

### Functions

```javascript
// Function declaration
function add(a, b) {
    return a + b;
}

// Function expression
const multiply = function(a, b) {
    return a * b;
};

// Arrow function (ES6)
const subtract = (a, b) => a - b;
```

### Conditionals

```javascript
if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}

// Ternary operator
const status = age >= 18 ? "Adult" : "Minor";

// Switch statement
switch (day) {
    case "Monday":
        console.log("Start of week");
        break;
    case "Friday":
        console.log("End of week");
        break;
    default:
        console.log("Middle of week");
}
```

### Loops

```javascript
// For loop
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// While loop
while (count < 10) {
    count++;
}

// For...of loop (arrays)
for (const item of array) {
    console.log(item);
}

// For...in loop (objects)
for (const key in object) {
    console.log(key, object[key]);
}
```

## JavaScript ở đâu?

### Client-side (Browser)

Tạo tính tương tác cho websites, xử lý events, thay đổi DOM.

### Server-side (Node.js)

Xây dựng backend APIs, real-time applications, command-line tools.

### Mobile (React Native, Ionic)

Phát triển mobile apps đa nền tảng.

### Desktop (Electron)

Tạo desktop applications (VS Code, Slack, Discord).

## Tại sao học JavaScript?

- Dễ học cho beginners
- Cộng đồng lớn nhất trong lập trình
- Full-stack development với một ngôn ngữ
- Nhu cầu công việc cao
- Frameworks và libraries phong phú (React, Vue, Angular, Node.js)
- Liên tục phát triển với các tính năng mới

JavaScript là ngôn ngữ bắt buộc phải biết cho bất kỳ web developer nào trong thời đại hiện nay!