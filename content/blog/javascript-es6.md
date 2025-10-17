---
title: "ES6+ Features - JavaScript hiện đại"
date: 2025-10-14
category: "JavaScript"
image: "images/jsES6.jpg"
description: "ES6+ đã cách mạng hóa JavaScript với các tính năng như Let/Const, Arrow Functions, Template Literals, Destructuring, Spread Operator, Classes, Modules, Optional Chaining và nhiều hơn nữa. Làm chủ JavaScript hiện đại!"
---

ES6 (ECMAScript 2015) và các phiên bản sau đã mang đến nhiều tính năng mới giúp JavaScript trở nên mạnh mẽ và dễ sử dụng hơn.

## Let và Const

Thay thế cho `var` với block scope tốt hơn.

```javascript
// let - có thể thay đổi
let count = 0;
count = 1;

// const - không thể reassign
const PI = 3.14159;
// PI = 3.14; // Error!

// Nhưng có thể modify object/array
const user = { name: 'John' };
user.name = 'Jane'; // OK
user.age = 30;      // OK
```

## Arrow Functions

Cú pháp ngắn gọn cho functions.

```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Với một parameter, bỏ được ngoặc
const square = x => x * x;

// Nhiều dòng cần return
const calculate = (a, b) => {
    const sum = a + b;
    return sum * 2;
};

// Arrow function không có 'this' riêng
const obj = {
    name: 'Object',
    regular: function() {
        console.log(this.name); // 'Object'
    },
    arrow: () => {
        console.log(this.name); // undefined hoặc global
    }
};
```

## Template Literals

String interpolation và multi-line strings.

```javascript
const name = 'John';
const age = 30;

// Old way
const message = 'Hello, my name is ' + name + ' and I am ' + age + ' years old.';

// Template literal
const message = `Hello, my name is ${name} and I am ${age} years old.`;

// Multi-line
const html = `
    <div class="card">
        <h2>${name}</h2>
        <p>Age: ${age}</p>
    </div>
`;

// Expressions
const result = `2 + 2 = ${2 + 2}`; // "2 + 2 = 4"
```

## Destructuring

Giải nén values từ arrays và objects.

### Array Destructuring

```javascript
const colors = ['red', 'green', 'blue'];

// Old way
const first = colors[0];
const second = colors[1];

// Destructuring
const [first, second, third] = colors;

// Skip elements
const [, , third] = colors;

// Rest operator
const [first, ...others] = colors;
console.log(others); // ['green', 'blue']

// Default values
const [a, b, c, d = 'yellow'] = colors;
```

### Object Destructuring

```javascript
const user = {
    name: 'John',
    age: 30,
    email: 'john@example.com'
};

// Old way
const name = user.name;
const age = user.age;

// Destructuring
const { name, age, email } = user;

// Rename variables
const { name: userName, age: userAge } = user;

// Default values
const { name, age, country = 'USA' } = user;

// Nested destructuring
const { address: { city, street } } = user;

// Function parameters
function greet({ name, age }) {
    console.log(`Hello ${name}, you are ${age} years old`);
}

greet(user);
```

## Spread Operator

Mở rộng arrays và objects.

```javascript
// Array spread
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Copy array
const copy = [...arr1];

// Object spread
const user = { name: 'John', age: 30 };
const updatedUser = { ...user, age: 31, city: 'NYC' };
// { name: 'John', age: 31, city: 'NYC' }

// Merge objects
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 3, c: 4 }

// Function arguments
const numbers = [1, 2, 3, 4, 5];
Math.max(...numbers); // 5
```

## Rest Parameters

Thu thập nhiều arguments thành array.

```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2, 3, 4, 5); // 15

// Combine với regular parameters
function multiply(multiplier, ...numbers) {
    return numbers.map(num => num * multiplier);
}

multiply(2, 1, 2, 3); // [2, 4, 6]
```

## Default Parameters

```javascript
function greet(name = 'Guest', greeting = 'Hello') {
    console.log(`${greeting}, ${name}!`);
}

greet(); // "Hello, Guest!"
greet('John'); // "Hello, John!"
greet('Jane', 'Hi'); // "Hi, Jane!"

// Default có thể là expression
function createUser(name, role = 'user', id = Date.now()) {
    return { name, role, id };
}
```

## Enhanced Object Literals

```javascript
const name = 'John';
const age = 30;

// Old way
const user = {
    name: name,
    age: age,
    greet: function() {
        console.log('Hello');
    }
};

// ES6 shorthand
const user = {
    name,
    age,
    greet() {
        console.log('Hello');
    }
};

// Computed property names
const prop = 'email';
const user = {
    [prop]: 'john@example.com',
    ['is' + 'Admin']: true
};
```

## Classes

Cú pháp OOP dễ đọc hơn.

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        console.log(`Hello, I'm ${this.name}`);
    }
    
    // Static method
    static create(name, age) {
        return new Person(name, age);
    }
    
    // Getter
    get info() {
        return `${this.name}, ${this.age}`;
    }
    
    // Setter
    set fullName(value) {
        this.name = value;
    }
}

// Inheritance
class Developer extends Person {
    constructor(name, age, language) {
        super(name, age);
        this.language = language;
    }
    
    code() {
        console.log(`Coding in ${this.language}`);
    }
}

const dev = new Developer('John', 30, 'JavaScript');
dev.greet(); // "Hello, I'm John"
dev.code();  // "Coding in JavaScript"
```

## Modules

Import/Export để tổ chức code.

```javascript
// math.js
export const PI = 3.14159;

export function add(a, b) {
    return a + b;
}

export function multiply(a, b) {
    return a * b;
}

// Default export
export default function subtract(a, b) {
    return a - b;
}

// main.js
import subtract, { add, multiply, PI } from './math.js';

// Import all
import * as math from './math.js';
console.log(math.add(2, 3));

// Rename imports
import { add as addition } from './math.js';
```

## Array Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// find - tìm element đầu tiên thỏa điều kiện
const found = numbers.find(n => n > 3); // 4

// findIndex
const index = numbers.findIndex(n => n > 3); // 3

// includes
numbers.includes(3); // true

// Array.from
Array.from('hello'); // ['h', 'e', 'l', 'l', 'o']
Array.from({ length: 3 }, (_, i) => i); // [0, 1, 2]
```

## Optional Chaining (?.)

```javascript
const user = {
    name: 'John',
    address: {
        city: 'NYC'
    }
};

// Old way
const street = user.address && user.address.street;

// Optional chaining
const street = user.address?.street; // undefined (no error)
const zip = user.address?.zip?.code; // undefined

// With methods
user.greet?.(); // Chỉ gọi nếu method tồn tại

// With arrays
const firstItem = arr?.[0];
```

## Nullish Coalescing (??)

```javascript
const value = null;

// || returns first truthy value
const result1 = value || 'default'; // 'default'
const result2 = 0 || 'default';     // 'default' (0 is falsy)

// ?? returns first non-nullish value (not null/undefined)
const result3 = value ?? 'default'; // 'default'
const result4 = 0 ?? 'default';     // 0 (0 is not nullish)
```

ES6+ đã làm JavaScript hiện đại và mạnh mẽ hơn rất nhiều, giúp developers viết code clean và hiệu quả hơn!