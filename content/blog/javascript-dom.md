---
title: "DOM Manipulation - Tương tác với HTML bằng JavaScript"
date: 2025-10-19
category: "JavaScript"
image: "images/jsdom.jpg"
description: "Document Object Model (DOM) là cầu nối giữa JavaScript và HTML, cho phép tạo trang web động và tương tác. Học cách selecting elements, manipulating content, styling, event handling và xây dựng Todo List thực tế."
---

Document Object Model (DOM) là cầu nối giữa JavaScript và HTML, cho phép chúng ta tạo ra các trang web động và tương tác.

## DOM là gì?

DOM là cấu trúc cây (tree structure) đại diện cho trang HTML. Mỗi element, attribute, và text đều là một node trong cây này.

```
document
  └── html
      ├── head
      │   └── title
      └── body
          ├── h1
          └── div
              ├── p
              └── button
```

## Selecting Elements

### getElementById

```javascript
const header = document.getElementById('main-header');
```

### querySelector (trả về element đầu tiên)

```javascript
const firstButton = document.querySelector('.btn');
const emailInput = document.querySelector('input[type="email"]');
```

### querySelectorAll (trả về NodeList)

```javascript
const allButtons = document.querySelectorAll('.btn');
allButtons.forEach(btn => {
    console.log(btn);
});
```

### Các methods khác

```javascript
document.getElementsByClassName('card'); // HTMLCollection
document.getElementsByTagName('p');      // HTMLCollection
```

## Manipulating Content

### innerHTML vs textContent

```javascript
const div = document.querySelector('#content');

// innerHTML - có thể chứa HTML tags
div.innerHTML = '<strong>Bold text</strong>';

// textContent - chỉ text thuần
div.textContent = 'Plain text';

// innerText - giống textContent nhưng tôn trọng styling
div.innerText = 'Visible text';
```

## Modifying Attributes

```javascript
const img = document.querySelector('img');

// Get attribute
img.getAttribute('src');

// Set attribute
img.setAttribute('src', 'new-image.jpg');
img.setAttribute('alt', 'Description');

// Remove attribute
img.removeAttribute('title');

// Direct property access
img.src = 'another-image.jpg';
img.alt = 'Another description';
```

## Styling Elements

### Inline styles

```javascript
const box = document.querySelector('.box');

box.style.backgroundColor = 'blue';
box.style.width = '200px';
box.style.fontSize = '18px';
```

### CSS Classes

```javascript
const element = document.querySelector('.card');

// Add class
element.classList.add('active');

// Remove class
element.classList.remove('hidden');

// Toggle class
element.classList.toggle('highlight');

// Check if has class
if (element.classList.contains('active')) {
    console.log('Element is active');
}

// Replace class
element.classList.replace('old-class', 'new-class');
```

## Creating and Adding Elements

```javascript
// Create new element
const newDiv = document.createElement('div');
newDiv.textContent = 'New content';
newDiv.classList.add('card');

// Append to parent (cuối cùng)
document.body.appendChild(newDiv);

// Prepend (đầu tiên)
document.body.prepend(newDiv);

// Insert before
const referenceNode = document.querySelector('.reference');
referenceNode.parentNode.insertBefore(newDiv, referenceNode);

// Modern methods
document.body.append(newDiv);           // Cuối
document.body.prepend(newDiv);          // Đầu
referenceNode.before(newDiv);           // Trước element
referenceNode.after(newDiv);            // Sau element
```

## Removing Elements

```javascript
const element = document.querySelector('.to-remove');

// Modern way
element.remove();

// Old way
element.parentNode.removeChild(element);
```

## Event Handling

### addEventListener

```javascript
const button = document.querySelector('#myButton');

button.addEventListener('click', function(event) {
    console.log('Button clicked!');
    console.log(event.target); // Element được click
});

// Arrow function
button.addEventListener('click', (e) => {
    e.preventDefault(); // Ngăn hành động mặc định
    console.log('Clicked!');
});
```

### Common Events

```javascript
// Mouse events
element.addEventListener('click', handler);
element.addEventListener('dblclick', handler);
element.addEventListener('mouseenter', handler);
element.addEventListener('mouseleave', handler);

// Keyboard events
input.addEventListener('keydown', handler);
input.addEventListener('keyup', handler);
input.addEventListener('keypress', handler);

// Form events
form.addEventListener('submit', handler);
input.addEventListener('input', handler);
input.addEventListener('change', handler);
input.addEventListener('focus', handler);
input.addEventListener('blur', handler);

// Window events
window.addEventListener('load', handler);
window.addEventListener('resize', handler);
window.addEventListener('scroll', handler);
```

### Event Object

```javascript
element.addEventListener('click', (event) => {
    console.log(event.type);        // 'click'
    console.log(event.target);      // Element được click
    console.log(event.currentTarget); // Element có listener
    console.log(event.clientX);     // Mouse X position
    console.log(event.clientY);     // Mouse Y position
    
    event.preventDefault();  // Ngăn hành động mặc định
    event.stopPropagation(); // Ngăn event bubbling
});
```

## Ví dụ thực tế

### Todo List

```javascript
const todoForm = document.querySelector('#todo-form');
const todoInput = document.querySelector('#todo-input');
const todoList = document.querySelector('#todo-list');

todoForm.addEventListener('submit', (e) => {
    e.preventDefault();
    
    const todoText = todoInput.value.trim();
    if (!todoText) return;
    
    // Tạo todo item
    const li = document.createElement('li');
    li.textContent = todoText;
    
    // Tạo delete button
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = 'Delete';
    deleteBtn.addEventListener('click', () => {
        li.remove();
    });
    
    li.appendChild(deleteBtn);
    todoList.appendChild(li);
    
    todoInput.value = ''; // Clear input
});
```

### Dark Mode Toggle

```javascript
const toggleBtn = document.querySelector('#dark-mode-toggle');

toggleBtn.addEventListener('click', () => {
    document.body.classList.toggle('dark-mode');
    
    const isDark = document.body.classList.contains('dark-mode');
    toggleBtn.textContent = isDark ? '☀️ Light Mode' : '🌙 Dark Mode';
    
    // Lưu preference
    localStorage.setItem('darkMode', isDark);
});

// Load preference
if (localStorage.getItem('darkMode') === 'true') {
    document.body.classList.add('dark-mode');
}
```

DOM manipulation là kỹ năng cốt lõi của JavaScript, giúp tạo ra các trang web tương tác và động.