---
title: "Async/Await và Promise trong JavaScript"
date: 2025-10-10T07:00:00Z
draft: false
tags: ["JavaScript", "Async", "Promise", "ES6"]
categories: ["JavaScript"]
author: "Nguyễn Tiến Dũng"
description: "Tìm hiểu về Promise và Async/Await - xử lý bất đồng bộ trong JavaScript một cách hiện đại và dễ đọc"
summary: "Promise xử lý các tác vụ bất đồng bộ trong JavaScript. Async/Await giúp viết code bất đồng bộ theo phong cách đồng bộ."
---
<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#giới-thiệu">Giới thiệu</a></li>
    <li><a href="#promise-là-gì">Promise là gì?</a></li>
    <li><a href="#ví-dụ-thực-tế-với-promise">Ví dụ thực tế với Promise</a></li>
    <li><a href="#asyncawait">Async/Await</a></li>
    <li><a href="#ví-dụ-thực-tế-với-asyncawait">Ví dụ thực tế với Async/Await</a></li>
    <li><a href="#error-handling">Error Handling</a></li>
    <li><a href="#promise-methods">Promise Methods</a></li>
    <li><a href="#patterns-và-best-practices">Patterns và Best Practices</a></li>
    <li><a href="#ví-dụ-ứng-dụng-thực-tế">Ví dụ ứng dụng thực tế</a></li>
    <li><a href="#common-mistakes-lỗi-thường-gặp">Common Mistakes (Lỗi thường gặp)</a></li>
    <li><a href="#so-sánh-tổng-hợp">So sánh tổng hợp</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## Giới thiệu

JavaScript là ngôn ngữ **single-threaded** (đơn luồng), nhưng cần xử lý nhiều tác vụ bất đồng bộ như:
- Gọi API
- Đọc/ghi file
- Timeout/Interval
- Event handling

**Promise** và **Async/Await** là giải pháp hiện đại để xử lý các tác vụ này một cách dễ đọc và dễ bảo trì.

---

## Promise là gì?

Promise là một **object** đại diện cho kết quả của một tác vụ bất đồng bộ trong tương lai.

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Promise là <strong>game changer</strong> trong JavaScript async programming! Trước ES6, chúng ta dùng callbacks → <strong>callback hell</strong> (pyramid of doom). Promise giải quyết vấn đề này với <strong>chaining</strong> và error handling tốt hơn. Và async/await làm code trở nên <strong>readable như synchronous code</strong> nhưng vẫn non-blocking!</p>
</div>

### 3 trạng thái của Promise:

1. **Pending** (đang chờ) - Trạng thái ban đầu
2. **Fulfilled** (thành công) - Tác vụ hoàn thành thành công
3. **Rejected** (thất bại) - Tác vụ bị lỗi

### Cú pháp cơ bản

```javascript
const promise = new Promise((resolve, reject) => {
  // Thực hiện tác vụ bất đồng bộ
  const success = true;
  
  if (success) {
    resolve('Thành công!'); // Chuyển sang Fulfilled
  } else {
    reject('Có lỗi xảy ra!'); // Chuyển sang Rejected
  }
});

// Sử dụng Promise
promise
  .then(result => console.log(result))    // Xử lý khi thành công
  .catch(error => console.error(error));  // Xử lý khi lỗi
```

---

## Ví dụ thực tế với Promise

### 1. Giả lập gọi API

```javascript
function fetchUser(userId) {
  return new Promise((resolve, reject) => {
    console.log('Đang tải dữ liệu user...');
    
    setTimeout(() => {
      if (userId > 0) {
        resolve({
          id: userId,
          name: 'Nguyễn Văn A',
          email: 'user@example.com'
        });
      } else {
        reject('User ID không hợp lệ!');
      }
    }, 2000); // Giả lập delay 2 giây
  });
}

// Sử dụng
fetchUser(1)
  .then(user => {
    console.log('User:', user);
    // Output sau 2s: User: { id: 1, name: 'Nguyễn Văn A', ... }
  })
  .catch(error => {
    console.error('Lỗi:', error);
  });
```

### 2. Chain Promises (Xử lý tuần tự)

```javascript
function step1() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('Bước 1 hoàn thành');
      resolve('Dữ liệu từ bước 1');
    }, 1000);
  });
}

function step2(data) {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('Bước 2 hoàn thành với:', data);
      resolve('Dữ liệu từ bước 2');
    }, 1000);
  });
}

function step3(data) {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log('Bước 3 hoàn thành với:', data);
      resolve('Kết quả cuối cùng');
    }, 1000);
  });
}

// Chain promises
step1()
  .then(result1 => step2(result1))
  .then(result2 => step3(result2))
  .then(finalResult => {
    console.log('Hoàn thành:', finalResult);
  })
  .catch(error => {
    console.error('Có lỗi:', error);
  });

// Output:
// Bước 1 hoàn thành
// Bước 2 hoàn thành với: Dữ liệu từ bước 1
// Bước 3 hoàn thành với: Dữ liệu từ bước 2
// Hoàn thành: Kết quả cuối cùng
```

### 3. Promise.all() - Chạy song song

```javascript
const promise1 = new Promise(resolve => {
  setTimeout(() => resolve('Kết quả 1'), 1000);
});

const promise2 = new Promise(resolve => {
  setTimeout(() => resolve('Kết quả 2'), 2000);
});

const promise3 = new Promise(resolve => {
  setTimeout(() => resolve('Kết quả 3'), 1500);
});

// Chờ tất cả promises hoàn thành
Promise.all([promise1, promise2, promise3])
  .then(results => {
    console.log('Tất cả hoàn thành:', results);
    // Output sau 2s: ['Kết quả 1', 'Kết quả 2', 'Kết quả 3']
  })
  .catch(error => {
    console.error('Có promise bị lỗi:', error);
  });
```

---

## Async/Await

**Async/Await** là cú pháp mới (ES2017) giúp viết code bất đồng bộ trông giống code đồng bộ, dễ đọc hơn.

### Cú pháp cơ bản

```javascript
// Khai báo async function
async function getData() {
  // await chờ Promise resolve
  const result = await someAsyncOperation();
  return result;
}

// async function luôn return một Promise
getData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```
<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>await chỉ hoạt động trong async function!</strong> Dùng await ở top-level (ngoài async function) → <code>SyntaxError</code>. Và nhớ: <strong>async function LUÔN return Promise</strong>, kể cả khi bạn return primitive value. Điều này quan trọng khi chain async functions!</p>
</div>

### So sánh Promise vs Async/Await

**Với Promise:**

```javascript
function getUser() {
  return fetchUser(1)
    .then(user => {
      console.log('User:', user);
      return fetchPosts(user.id);
    })
    .then(posts => {
      console.log('Posts:', posts);
      return posts;
    })
    .catch(error => {
      console.error('Lỗi:', error);
    });
}
```

**Với Async/Await (dễ đọc hơn):**

```javascript
async function getUser() {
  try {
    const user = await fetchUser(1);
    console.log('User:', user);
    
    const posts = await fetchPosts(user.id);
    console.log('Posts:', posts);
    
    return posts;
  } catch (error) {
    console.error('Lỗi:', error);
  }
}
```

---

## Ví dụ thực tế với Async/Await

### 1. Fetch API

```javascript
async function getUserData(userId) {
  try {
    // Gọi API để lấy user
    const userResponse = await fetch(`https://api.example.com/users/${userId}`);
    const user = await userResponse.json();
    console.log('User:', user);
    
    // Gọi API để lấy posts của user
    const postsResponse = await fetch(`https://api.example.com/users/${userId}/posts`);
    const posts = await postsResponse.json();
    console.log('Posts:', posts);
    
    return { user, posts };
  } catch (error) {
    console.error('Lỗi khi lấy dữ liệu:', error);
    throw error;
  }
}

// Sử dụng
getUserData(1)
  .then(data => console.log('Dữ liệu đầy đủ:', data))
  .catch(error => console.error('Error:', error));
```

### 2. Xử lý nhiều requests song song

```javascript
async function getAllData() {
  try {
    console.log('Bắt đầu tải dữ liệu...');
    
    // Chạy song song để nhanh hơn
    const [users, posts, comments] = await Promise.all([
      fetch('https://api.example.com/users').then(r => r.json()),
      fetch('https://api.example.com/posts').then(r => r.json()),
      fetch('https://api.example.com/comments').then(r => r.json())
    ]);
    
    console.log('Tất cả dữ liệu đã tải xong!');
    
    return { users, posts, comments };
  } catch (error) {
    console.error('Lỗi:', error);
    throw error;
  }
}

getAllData()
  .then(data => console.log('Data:', data))
  .catch(error => console.error('Error:', error));
```

### 3. Retry logic (thử lại khi lỗi)

```javascript
async function fetchWithRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      console.log(`Thử lần ${i + 1}...`);
      const response = await fetch(url);
      
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      
      const data = await response.json();
      console.log('Thành công!');
      return data;
    } catch (error) {
      console.error(`Lần ${i + 1} thất bại:`, error.message);
      
      if (i === maxRetries - 1) {
        throw new Error('Đã thử tối đa số lần cho phép');
      }
      
      // Đợi 1 giây trước khi thử lại
      await new Promise(resolve => setTimeout(resolve, 1000));
    }
  }
}

// Sử dụng
fetchWithRetry('https://api.example.com/data')
  .then(data => console.log('Data:', data))
  .catch(error => console.error('Final error:', error));
```

---

## Error Handling

### Try-Catch trong Async/Await

```javascript
async function riskyOperation() {
  try {
    const data1 = await fetchData1();
    console.log('Data 1:', data1);
    
    const data2 = await fetchData2();
    console.log('Data 2:', data2);
    
    const result = await processData(data1, data2);
    return result;
  } catch (error) {
    // Bắt tất cả lỗi trong try block
    console.error('Có lỗi xảy ra:', error);
    
    // Có thể throw lại để caller xử lý
    throw error;
    
    // Hoặc return giá trị mặc định
    // return null;
  } finally {
    // Code trong finally luôn chạy
    console.log('Cleanup...');
  }
}
```
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Luôn wrap async operations trong <code>try/catch</code> để handle errors! Unhandled promise rejections có thể crash Node.js apps. Với async/await, dùng try/catch. Với Promises, dùng <code>.catch()</code>. Và quan trọng: <strong>NEVER ignore errors</strong> - ít nhất phải log chúng để debug!</p>
</div>

### Xử lý lỗi riêng biệt

```javascript
async function fetchMultipleData() {
  try {
    const user = await fetchUser().catch(error => {
      console.error('Lỗi khi lấy user:', error);
      return null; // Return giá trị mặc định
    });
    
    const posts = await fetchPosts().catch(error => {
      console.error('Lỗi khi lấy posts:', error);
      return []; // Return array rỗng
    });
    
    return { user, posts };
  } catch (error) {
    console.error('Lỗi không mong đợi:', error);
  }
}
```

---

## Promise Methods

### Promise.all()

Chờ **tất cả** promises hoàn thành. Nếu có 1 promise reject, toàn bộ bị reject.

```javascript
async function loadAllData() {
  try {
    const [users, products, orders] = await Promise.all([
      fetchUsers(),
      fetchProducts(),
      fetchOrders()
    ]);
    
    return { users, products, orders };
  } catch (error) {
    console.error('Có ít nhất 1 request bị lỗi:', error);
  }
}
```

### Promise.allSettled()

Chờ **tất cả** promises hoàn thành, không quan tâm fulfilled hay rejected.

```javascript
async function loadDataSafely() {
  const results = await Promise.allSettled([
    fetchUsers(),
    fetchProducts(),
    fetchOrders()
  ]);
  
  results.forEach((result, index) => {
    if (result.status === 'fulfilled') {
      console.log(`Request ${index} thành công:`, result.value);
    } else {
      console.error(`Request ${index} thất bại:`, result.reason);
    }
  });
}
```

### Promise.race()

Trả về kết quả của promise **nhanh nhất** (fulfilled hoặc rejected đều được).

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
  const fetchPromise = fetch(url);
  const timeoutPromise = new Promise((_, reject) => {
    setTimeout(() => reject(new Error('Timeout!')), timeout);
  });
  
  try {
    const response = await Promise.race([fetchPromise, timeoutPromise]);
    return await response.json();
  } catch (error) {
    console.error('Lỗi hoặc timeout:', error);
    throw error;
  }
}
```

### Promise.any()

Trả về promise **fulfilled đầu tiên**. Chỉ reject khi **tất cả** đều rejected.

```javascript
async function fetchFromMultipleSources() {
  try {
    const data = await Promise.any([
      fetch('https://api1.example.com/data'),
      fetch('https://api2.example.com/data'),
      fetch('https://api3.example.com/data')
    ]);
    
    return await data.json();
  } catch (error) {
    console.error('Tất cả sources đều thất bại');
  }
}
```

---

## Patterns và Best Practices

### 1. Sequential vs Parallel Execution

**Sequential (chậm hơn):**

```javascript
async function sequential() {
  const user = await fetchUser();      // 2s
  const posts = await fetchPosts();    // 2s
  const comments = await fetchComments(); // 2s
  // Tổng: 6 giây
  
  return { user, posts, comments };
}
```

**Parallel (nhanh hơn):**

```javascript
async function parallel() {
  const [user, posts, comments] = await Promise.all([
    fetchUser(),      // \
    fetchPosts(),     //  } Chạy đồng thời
    fetchComments()   // /
  ]);
  // Tổng: 2 giây (thời gian của request chậm nhất)
  
  return { user, posts, comments };
}
```

### 2. Error Boundaries

```javascript
async function safeOperation() {
  let result = null;
  
  try {
    result = await riskyOperation();
  } catch (error) {
    console.error('Operation failed:', error);
    // Log to monitoring service
    logError(error);
    // Return default value
    result = getDefaultValue();
  }
  
  return result;
}
```

### 3. Timeout Pattern

```javascript
function withTimeout(promise, timeoutMs) {
  return Promise.race([
    promise,
    new Promise((_, reject) =>
      setTimeout(() => reject(new Error('Timeout')), timeoutMs)
    )
  ]);
}

// Sử dụng
async function fetchWithTimeout() {
  try {
    const data = await withTimeout(fetch('/api/data'), 3000);
    return await data.json();
  } catch (error) {
    if (error.message === 'Timeout') {
      console.error('Request quá lâu!');
    }
    throw error;
  }
}
```

---

## Ví dụ ứng dụng thực tế

### Todo App với API

```javascript
class TodoAPI {
  constructor(baseURL) {
    this.baseURL = baseURL;
  }
  
  async getAllTodos() {
    try {
      const response = await fetch(`${this.baseURL}/todos`);
      if (!response.ok) throw new Error('Failed to fetch todos');
      return await response.json();
    } catch (error) {
      console.error('Error fetching todos:', error);
      throw error;
    }
  }
  
  async createTodo(todo) {
    try {
      const response = await fetch(`${this.baseURL}/todos`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(todo)
      });
      
      if (!response.ok) throw new Error('Failed to create todo');
      return await response.json();
    } catch (error) {
      console.error('Error creating todo:', error);
      throw error;
    }
  }
  
  async updateTodo(id, updates) {
    try {
      const response = await fetch(`${this.baseURL}/todos/${id}`, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(updates)
      });
      
      if (!response.ok) throw new Error('Failed to update todo');
      return await response.json();
    } catch (error) {
      console.error('Error updating todo:', error);
      throw error;
    }
  }
  
  async deleteTodo(id) {
    try {
      const response = await fetch(`${this.baseURL}/todos/${id}`, {
        method: 'DELETE'
      });
      
      if (!response.ok) throw new Error('Failed to delete todo');
      return true;
    } catch (error) {
      console.error('Error deleting todo:', error);
      throw error;
    }
  }
}

// Sử dụng
const api = new TodoAPI('https://jsonplaceholder.typicode.com');

async function manageTodos() {
  try {
    // Lấy tất cả todos
    const todos = await api.getAllTodos();
    console.log('Todos:', todos.slice(0, 3));
    
    // Tạo todo mới
    const newTodo = await api.createTodo({
      title: 'Learn Async/Await',
      completed: false,
      userId: 1
    });
    console.log('New todo:', newTodo);
    
    // Cập nhật todo
    const updated = await api.updateTodo(newTodo.id, {
      completed: true
    });
    console.log('Updated todo:', updated);
    
    // Xóa todo
    await api.deleteTodo(newTodo.id);
    console.log('Todo deleted');
    
  } catch (error) {
    console.error('Error managing todos:', error);
  }
}

manageTodos();
```

---

## Common Mistakes (Lỗi thường gặp)

### 1. Quên await

```javascript
// ❌ Sai - Quên await
async function wrong() {
  const data = fetchData(); // data là Promise, không phải dữ liệu!
  console.log(data); // Promise { <pending> }
}

// ✅ Đúng
async function correct() {
  const data = await fetchData();
  console.log(data); // Dữ liệu thực
}
```

### 2. Await trong loop không cần thiết

```javascript
// ❌ Chậm - Chạy tuần tự
async function slow() {
  const results = [];
  for (const id of [1, 2, 3, 4, 5]) {
    const data = await fetchData(id); // Chờ từng cái
    results.push(data);
  }
  return results;
}

// ✅ Nhanh - Chạy song song
async function fast() {
  const promises = [1, 2, 3, 4, 5].map(id => fetchData(id));
  return await Promise.all(promises);
}
```

### 3. Không xử lý lỗi

```javascript
// ❌ Sai - Lỗi không được bắt
async function noErrorHandling() {
  const data = await fetchData(); // Nếu lỗi sẽ crash
  return data;
}

// ✅ Đúng
async function withErrorHandling() {
  try {
    const data = await fetchData();
    return data;
  } catch (error) {
    console.error('Error:', error);
    return null;
  }
}
```

---

## So sánh tổng hợp

| Tiêu chí | Callback | Promise | Async/Await |
|----------|----------|---------|-------------|
| **Cú pháp** | Phức tạp | Tốt | Rất tốt |
| **Callback Hell** | Có | Không | Không |
| **Error Handling** | Khó | try/catch | try/catch |
| **Debugging** | Khó | Trung bình | Dễ |
| **Đọc code** | Khó | Tốt | Rất tốt |
| **Browser Support** | 100% | >95% | >93% |

---
---

## 🐛 Lỗi thường gặp với Async/Await & Promise

### ❌ Lỗi 1: Quên await → Promise không resolve

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Forgot await</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Quên <code>await</code> trước async function → nhận Promise object thay vì resolved value!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - Quên await
async function fetchUser() {
    const response = await fetch('/api/user');
    return response.json();
}

async function displayUser() {
    const user = fetchUser();  // ❌ Quên await!
    console.log(user);         // Promise {<pending>} 
    console.log(user.name);    // undefined! 🤯
}

displayUser();
```

**Output:**
```
Promise {<pending>}
undefined
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Thêm await
async function fetchUser() {
    const response = await fetch('/api/user');
    return response.json();
}

async function displayUser() {
    const user = await fetchUser();  // ✅ Có await!
    console.log(user);               // { name: "John", ... }
    console.log(user.name);          // "John"
}

displayUser();
```

**💡 Rule of thumb:** Nếu gọi async function → luôn await (trừ khi muốn Promise object)

---

### ❌ Lỗi 2: Không catch errors → Unhandled rejection

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">UnhandledPromiseRejection</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Async operation fail mà không có try/catch hoặc .catch() → <strong>unhandled promise rejection</strong> → có thể crash app!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - Không có error handling
async function fetchData() {
    const response = await fetch('/api/data');  // Có thể fail!
    const data = await response.json();
    return data;
}

// Nếu fetch fail → UnhandledPromiseRejection warning
fetchData();  // ❌ Không catch error!
```

**Error:**
```
(node:12345) UnhandledPromiseRejectionWarning: TypeError: Failed to fetch
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Cách 1: try/catch
async function fetchData() {
    try {
        const response = await fetch('/api/data');
        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Fetch failed:', error);
        return null; // Hoặc throw error để caller xử lý
    }
}

// ✅ ĐÚNG - Cách 2: .catch() chain
fetchData()
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));

// ✅ ĐÚNG - Cách 3: Wrapper function
async function safelyFetchData() {
    try {
        return await fetchData();
    } catch (error) {
        console.error('Failed to fetch data:', error);
        return null;
    }
}
```

---

### ❌ Lỗi 3: Sequential thay vì Parallel → Chậm!

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2p solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Performance Issue</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Await từng operation độc lập → chạy tuần tự thay vì song song → <strong>waste time</strong>!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - Sequential (chạy tuần tự)
async function fetchAllData() {
    const user = await fetchUser();      // 1s
    const posts = await fetchPosts();    // 1s
    const comments = await fetchComments(); // 1s
    
    return { user, posts, comments };
    // Tổng: 3 giây! 🐌
}
```

**Timeline:**
```
fetchUser()    [====1s====]
fetchPosts()                [====1s====]
fetchComments()                          [====1s====]
Total: 3 seconds
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Parallel (chạy song song)
async function fetchAllData() {
    // Start tất cả cùng lúc
    const [user, posts, comments] = await Promise.all([
        fetchUser(),
        fetchPosts(),
        fetchComments()
    ]);
    
    return { user, posts, comments };
    // Tổng: 1 giây! 🚀
}

// ✅ HOẶC - Manual parallel
async function fetchAllData() {
    // Khởi động tất cả (không await ngay)
    const userPromise = fetchUser();
    const postsPromise = fetchPosts();
    const commentsPromise = fetchComments();
    
    // Đợi tất cả complete
    const user = await userPromise;
    const posts = await postsPromise;
    const comments = await commentsPromise;
    
    return { user, posts, comments };
}
```

**Timeline (parallel):**
```
fetchUser()    [====1s====]
fetchPosts()   [====1s====]
fetchComments()[====1s====]
Total: 1 second (3x faster!)
```

---

### ❌ Lỗi 4: Async function trong forEach → Không await!

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">forEach with async</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;"><code>forEach()</code> không wait cho async callbacks! Promises chạy nhưng không được awaited.</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - forEach không đợi async
async function processUsers(userIds) {
    userIds.forEach(async (id) => {
        const user = await fetchUser(id);
        await saveUser(user);
    });
    
    console.log('Done!'); // ❌ Chạy NGAY, không đợi!
    // Promises vẫn đang chạy ở background
}

processUsers([1, 2, 3]);
// Output: "Done!" (immediately)
// Promises chạy sau đó, không theo control
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Cách 1: for...of loop
async function processUsers(userIds) {
    for (const id of userIds) {
        const user = await fetchUser(id);
        await saveUser(user);
    }
    console.log('Done!'); // ✅ Chạy SAU KHI tất cả xong
}

// ✅ ĐÚNG - Cách 2: Promise.all (parallel)
async function processUsers(userIds) {
    await Promise.all(
        userIds.map(async (id) => {
            const user = await fetchUser(id);
            await saveUser(user);
        })
    );
    console.log('Done!'); // ✅ Chạy sau khi tất cả xong
}

// ✅ ĐÚNG - Cách 3: for await...of (với async iterables)
async function processUsers(userIds) {
    for await (const id of userIds) {
        const user = await fetchUser(id);
        await saveUser(user);
    }
    console.log('Done!');
}
```

**Comparison:**
```javascript
// Sequential (1 tại 1 thời điểm)
for (const id of userIds) {
    await process(id);  // Đợi xong mới tiếp tục
}

// Parallel (tất cả cùng lúc)
await Promise.all(
    userIds.map(id => process(id))
);
```
---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** Promise có 3 states nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>3 States của Promise:</strong></p>
    <ol style="margin: 0;">
      <li><strong>⏳ Pending:</strong> Initial state, chưa fulfilled hoặc rejected</li>
      <li><strong>✅ Fulfilled:</strong> Operation thành công, có value</li>
      <li><strong>❌ Rejected:</strong> Operation thất bại, có error reason</li>
    </ol>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #e3f2fd; border-radius: 4px;">💡 Promise chỉ chuyển state 1 lần: Pending → Fulfilled hoặc Pending → Rejected (immutable)</p>
  </div>
</details>

**Câu 2:** async function return gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 15px 0;"><strong>async function LUÔN return Promise!</strong></p>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 0;"><code>async function foo() {
    return 42;  // Tự động wrap trong Promise
}

foo(); // Promise {<fulfilled>: 42}
foo().then(x => console.log(x)); // 42

// Tương đương với:
function foo() {
    return Promise.resolve(42);
}</code></pre>
  </div>
</details>

**Câu 3:** Promise.all() vs Promise.race() vs Promise.allSettled()?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Method</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Khi nào resolve?</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Khi nào reject?</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>Promise.all()</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khi TẤT CẢ fulfilled</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khi 1 promise reject</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>Promise.race()</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khi promise ĐẦU TIÊN settled</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khi promise đầu tiên reject</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>Promise.allSettled()</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khi TẤT CẢ settled (không reject)</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">KHÔNG BAO GIỜ reject</td>
      </tr>
    </table>
  </div>
</details>

**Câu 4:** Khi nào dùng .then() chain, khi nào dùng async/await?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>⛓️ .then() chain:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Cần chain nhiều operations</li>
      <li>Mỗi step transform data khác nhau</li>
      <li>Functional programming style</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🎯 async/await:</strong></p>
    <ul style="margin: 0;">
      <li>✅ Code readable hơn (như synchronous)</li>
      <li>✅ Error handling dễ hơn (try/catch)</li>
      <li>✅ Debugging dễ hơn</li>
      <li>✅ Conditional logic phức tạp</li>
    </ul>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #d4edda; border-radius: 4px;">💡 Modern best practice: Prefer async/await!</p>
  </div>
</details>

**Câu 5:** Top-level await là gì? (ES2022)

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Top-level await (ES2022):</strong> Dùng await ở module scope (ngoài async function)</p>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 10px 0;"><code>// ✅ OK trong ES modules (type="module")
const data = await fetch('/api/data');
const config = await import('./config.json');

// Toàn bộ module block until await complete
export const results = await processData(data);</code></pre>
    <p style="margin: 10px 0 0 0;"><strong>⚠️ Chỉ hoạt động trong:</strong> ES modules, không phải scripts thường</p>
  </div>
</details>

</div>

## Kết luận

**Promise** và **Async/Await** đã thay đổi cách viết code bất đồng bộ trong JavaScript:

✅ **Code dễ đọc hơn** - Giống code đồng bộ  
✅ **Error handling tốt hơn** - try/catch thay vì callback error  
✅ **Tránh callback hell** - Không còn nested callbacks  
✅ **Dễ debug** - Stack trace rõ ràng hơn  

**Best Practices:**
- Luôn dùng `try/catch` với async/await
- Sử dụng `Promise.all()` cho parallel execution
- Avoid awaiting trong loops khi không cần thiết
- Return promises từ async functions
- Handle errors gracefully

**Quy tắc vàng:**
- Dùng **Async/Await** cho code mới - dễ đọc và maintain
- Dùng **Promise.all()** khi cần chạy nhiều tasks song song
- Luôn **handle errors** để tránh unhandled promise rejections

Hãy thực hành nhiều với async/await - đây là standard của JavaScript hiện đại!

---

## Bài tập thực hành

### Bài 1: Fetch API cơ bản

```javascript
// Viết function lấy thông tin user và posts của user đó
async function getUserWithPosts(userId) {
  // Code here
}

// Test
getUserWithPosts(1).then(console.log);
```

### Bài 2: Xử lý song song

```javascript
// Viết function load 3 resources song song
async function loadAllResources() {
  // Code here: fetch users, posts, và comments đồng thời
}
```

### Bài 3: Retry logic

```javascript
// Viết function retry khi gặp lỗi (tối đa 3 lần)
async function fetchWithRetry(url, maxRetries = 3) {
  // Code here
}
```

**Đáp án:**

```javascript
// Bài 1
async function getUserWithPosts(userId) {
  try {
    const user = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
      .then(r => r.json());
    const posts = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}/posts`)
      .then(r => r.json());
    return { user, posts };
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}

// Bài 2
async function loadAllResources() {
  const [users, posts, comments] = await Promise.all([
    fetch('https://jsonplaceholder.typicode.com/users').then(r => r.json()),
    fetch('https://jsonplaceholder.typicode.com/posts').then(r => r.json()),
    fetch('https://jsonplaceholder.typicode.com/comments').then(r => r.json())
  ]);
  return { users, posts, comments };
}

// Bài 3
async function fetchWithRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      return await fetch(url).then(r => r.json());
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      await new Promise(r => setTimeout(r, 1000 * (i + 1)));
    }
  }
}
```

---

## Tài liệu tham khảo

- [MDN - Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN - async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript.info - Promises](https://javascript.info/promise-basics)
- [JavaScript.info - Async/Await](https://javascript.info/async-await)
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">Nền tảng trước khi học async programming</p>
  </div>
</a>

<a href="/posts/bai7" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🌐</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">DOM Manipulation</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">Kết hợp async/await với DOM events</p>
  </div>
</a>

<a href="/posts" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">📚</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Xem tất cả bài viết</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">Khám phá thêm nhiều bài viết</p>
  </div>
</a>

</div>
