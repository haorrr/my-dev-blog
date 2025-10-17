---
title: "Asynchronous JavaScript - Callbacks, Promises, Async/Await"
date: 2025-10-17
category: "JavaScript"
image: "images/jsasync.jpg"
description: "Lập trình bất đồng bộ là khái niệm quan trọng trong JavaScript. Hiểu về Event Loop, vượt qua Callback Hell với Promises, và sử dụng Async/Await để viết code clean hơn. Bao gồm Promise.all(), Promise.race() và error handling."
---

Lập trình bất đồng bộ (asynchronous programming) là khái niệm quan trọng trong JavaScript, cho phép thực hiện các tác vụ mất thời gian mà không làm block code.

## JavaScript Event Loop

JavaScript là single-threaded, nghĩa là chỉ có một call stack. Event loop giúp JavaScript xử lý async operations.

### Hoạt động của Event Loop:

1. Code đồng bộ chạy trong call stack
2. Async operations (setTimeout, fetch) được gửi đến Web APIs
3. Khi hoàn thành, callbacks được đưa vào callback queue
4. Event loop kiểm tra call stack, nếu trống thì đưa callback từ queue vào

## Callbacks

Callback là function được truyền vào function khác để thực thi sau.

```javascript
function fetchData(callback) {
    setTimeout(() => {
        const data = { name: 'John', age: 30 };
        callback(data);
    }, 2000);
}

fetchData((data) => {
    console.log(data);
});
```

### Callback Hell

Khi có nhiều async operations lồng nhau:

```javascript
getData((data) => {
    processData(data, (processed) => {
        saveData(processed, (saved) => {
            sendEmail(saved, (result) => {
                console.log('Done!');
            });
        });
    });
});
```

**Vấn đề**: Code khó đọc, khó maintain, khó handle errors.

## Promises

Promise là object đại diện cho kết quả của async operation trong tương lai.

### States của Promise:

- **Pending**: Đang chờ
- **Fulfilled**: Thành công (resolved)
- **Rejected**: Thất bại

### Tạo Promise

```javascript
const myPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        const success = true;
        
        if (success) {
            resolve('Operation successful!');
        } else {
            reject('Operation failed!');
        }
    }, 2000);
});
```

### Sử dụng Promise

```javascript
myPromise
    .then((result) => {
        console.log(result); // Nếu thành công
        return 'Next step';
    })
    .then((data) => {
        console.log(data);
    })
    .catch((error) => {
        console.error(error); // Nếu thất bại
    })
    .finally(() => {
        console.log('Always runs');
    });
```

### Promise Chaining

```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => {
        console.log(data);
        return fetch(`https://api.example.com/user/${data.userId}`);
    })
    .then(response => response.json())
    .then(user => {
        console.log(user);
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

## Async/Await

Async/await là cú pháp hiện đại để làm việc với Promises, giúp code trông giống synchronous.

### Async Function

```javascript
async function fetchUser() {
    return 'User data'; // Tự động wrap trong Promise
}

// Tương đương với:
function fetchUser() {
    return Promise.resolve('User data');
}
```

### Await

```javascript
async function getData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        console.log(data);
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}

getData();
```

### Ví dụ thực tế

```javascript
async function getUserPosts(userId) {
    try {
        // Fetch user
        const userResponse = await fetch(`/api/users/${userId}`);
        const user = await userResponse.json();
        console.log('User:', user);
        
        // Fetch posts
        const postsResponse = await fetch(`/api/users/${userId}/posts`);
        const posts = await postsResponse.json();
        console.log('Posts:', posts);
        
        return { user, posts };
    } catch (error) {
        console.error('Error fetching data:', error);
        throw error;
    }
}

getUserPosts(1);
```

## Promise Methods

### Promise.all()

Chờ tất cả promises hoàn thành (parallel execution):

```javascript
async function fetchMultipleData() {
    try {
        const [users, posts, comments] = await Promise.all([
            fetch('/api/users').then(r => r.json()),
            fetch('/api/posts').then(r => r.json()),
            fetch('/api/comments').then(r => r.json())
        ]);
        
        console.log(users, posts, comments);
    } catch (error) {
        // Nếu bất kỳ promise nào fail
        console.error(error);
    }
}
```

### Promise.race()

Trả về promise đầu tiên hoàn thành (hoặc reject):

```javascript
const timeout = new Promise((_, reject) => {
    setTimeout(() => reject('Timeout!'), 5000);
});

const fetchData = fetch('/api/data');

Promise.race([fetchData, timeout])
    .then(response => console.log('Success!'))
    .catch(error => console.error(error));
```

### Promise.allSettled()

Chờ tất cả promises hoàn thành, không quan tâm success hay fail:

```javascript
const promises = [
    fetch('/api/users'),
    fetch('/api/invalid-endpoint'),
    fetch('/api/posts')
];

const results = await Promise.allSettled(promises);

results.forEach((result, index) => {
    if (result.status === 'fulfilled') {
        console.log(`Promise ${index} succeeded:`, result.value);
    } else {
        console.log(`Promise ${index} failed:`, result.reason);
    }
});
```

### Promise.any()

Trả về promise đầu tiên succeed:

```javascript
const servers = [
    fetch('https://server1.com/api'),
    fetch('https://server2.com/api'),
    fetch('https://server3.com/api')
];

try {
    const fastest = await Promise.any(servers);
    console.log('Fastest server responded:', fastest);
} catch (error) {
    console.log('All servers failed');
}
```

## Error Handling

### Try/Catch với Async/Await

```javascript
async function safeFunction() {
    try {
        const data = await riskyOperation();
        return data;
    } catch (error) {
        console.error('Error occurred:', error.message);
        // Handle error hoặc rethrow
        throw new Error('Operation failed');
    } finally {
        console.log('Cleanup code');
    }
}
```

## Best Practices

1. **Prefer async/await over .then()**: Code dễ đọc hơn
2. **Always handle errors**: Dùng try/catch hoặc .catch()
3. **Use Promise.all() for parallel operations**: Tiết kiệm thời gian
4. **Don't await in loops unnecessarily**: 

```javascript
// ❌ Slow - sequential
for (const id of ids) {
    await fetchUser(id);
}

// ✅ Fast - parallel
await Promise.all(ids.map(id => fetchUser(id)));
```

5. **Clean up resources**: Dùng finally block

Async/await làm cho async code trong JavaScript trở nên dễ đọc và dễ maintain hơn rất nhiều!