---
title: "Arrow Functions và ES6"
date: 2025-10-10T08:00:00Z
draft: false
tags: ["JavaScript", "ES6", "Programming"]
categories: ["JavaScript"]
author: "Nguyễn Tiến Dũng"
description: "Tìm hiểu về Arrow Functions trong ES6 - cú pháp ngắn gọn, this binding và cách sử dụng hiệu quả"
summary: "Arrow function là cách viết hàm ngắn gọn hơn trong ES6. Tìm hiểu cú pháp, this binding và cách sử dụng hiệu quả."
---
<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#giới-thiệu">Giới thiệu</a></li>
    <li><a href="#cú-pháp-cơ-bản">Cú pháp cơ bản</a></li>
    <li><a href="#sự-khác-biệt-về-this">Sự khác biệt về this</a></li>
    <li><a href="#sử-dụng-với-array-methods">Sử dụng với Array Methods</a></li>
    <li><a href="#khi-nào-nên-dùng">Khi nào nên dùng?</a></li>
    <li><a href="#so-sánh-tổng-hợp">So sánh tổng hợp</a></li>
    <li><a href="#ví-dụ-thực-tế">Ví dụ thực tế</a></li>
    <li><a href="#tips-và-best-practices">Tips và Best Practices</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## Giới thiệu

Arrow function là một trong những tính năng quan trọng nhất của ES6 (ECMAScript 2015). Nó cung cấp cú pháp ngắn gọn hơn để viết hàm trong JavaScript.

ES6 đã thêm nhiều tính năng mới: **let**, **const**, **template literals**, **destructuring**, và đặc biệt là **arrow functions**.

Arrow function không chỉ giúp code ngắn gọn mà còn có cách xử lý `this` khác biệt so với function thường.


---

## Cú pháp cơ bản

### Function thường vs Arrow Function

```javascript
// Function thường
function add(a, b) {
  return a + b;
}

// Arrow function - cú pháp đầy đủ
const add = (a, b) => {
  return a + b;
};

// Arrow function - cú pháp ngắn gọn (implicit return)
const add = (a, b) => a + b;

console.log(add(5, 3)); // Output: 8
```

### Một tham số

Khi chỉ có một tham số, có thể bỏ dấu ngoặc:

```javascript
// Không cần dấu ngoặc
const square = x => x * x;

console.log(square(4)); // Output: 16
console.log(square(7)); // Output: 49
```

### Không có tham số

Khi không có tham số, cần dấu ngoặc rỗng:

```javascript
const greet = () => console.log("Xin chào!");

greet(); // Output: Xin chào!

const getRandomNumber = () => Math.random();
console.log(getRandomNumber()); // Output: số ngẫu nhiên
```

---

## Sự khác biệt về `this`

Đây là điểm quan trọng nhất khi sử dụng arrow function!

### Function thường

```javascript
const person = {
  name: 'Dũng',
  age: 25,
  
  sayHi: function() {
    console.log('Xin chào, tôi là ' + this.name);
    console.log('Năm nay tôi ' + this.age + ' tuổi');
  }
};

person.sayHi();
// Output:
// Xin chào, tôi là Dũng
// Năm nay tôi 25 tuổi
```

### Arrow function kế thừa `this`

```javascript
const person = {
  name: 'Dũng',
  friends: ['An', 'Bình', 'Chi'],
  
  showFriends: function() {
    this.friends.forEach(friend => {
      // Arrow function kế thừa this từ showFriends
      console.log(this.name + ' là bạn với ' + friend);
    });
  }
};

person.showFriends();
// Output:
// Dũng là bạn với An
// Dũng là bạn với Bình
// Dũng là bạn với Chi
```

### So sánh với function thường

```javascript
const person = {
  name: 'Dũng',
  friends: ['An', 'Bình'],
  
  showFriendsWrong: function() {
    this.friends.forEach(function(friend) {
      // this ở đây KHÔNG trỏ đến person!
      console.log(this.name + ' là bạn với ' + friend);
    });
  }
};

person.showFriendsWrong();
// Output: undefined là bạn với An
//         undefined là bạn với Bình
```

---

## Sử dụng với Array Methods

Arrow function rất hữu ích với các phương thức của Array.

### Map - Biến đổi mảng

```javascript
const numbers = [1, 2, 3, 4, 5];

// Cách cũ
const doubled = numbers.map(function(n) {
  return n * 2;
});

// Arrow function - ngắn gọn hơn
const doubled = numbers.map(n => n * 2);

console.log(doubled); // [2, 4, 6, 8, 10]

// Ví dụ phức tạp hơn
const users = [
  { name: 'An', age: 25 },
  { name: 'Bình', age: 30 }
];

const names = users.map(user => user.name);
console.log(names); // ['An', 'Bình']
```

### Filter - Lọc mảng

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Lọc số chẵn
const evenNumbers = numbers.filter(n => n % 2 === 0);
console.log(evenNumbers); // [2, 4, 6, 8, 10]

// Lọc số lớn hơn 5
const bigNumbers = numbers.filter(n => n > 5);
console.log(bigNumbers); // [6, 7, 8, 9, 10]

// Ví dụ thực tế
const products = [
  { name: 'Laptop', price: 20000000 },
  { name: 'Mouse', price: 200000 },
  { name: 'Keyboard', price: 500000 }
];

const expensiveProducts = products.filter(p => p.price > 1000000);
console.log(expensiveProducts);
// [{ name: 'Laptop', price: 20000000 }]
```

### Reduce - Tính toán tổng hợp

```javascript
const numbers = [1, 2, 3, 4, 5];

// Tính tổng
const sum = numbers.reduce((total, n) => total + n, 0);
console.log(sum); // 15

// Tìm số lớn nhất
const max = numbers.reduce((max, n) => n > max ? n : max);
console.log(max); // 5

// Đếm số lần xuất hiện
const fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple'];

const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});

console.log(count);
// { apple: 3, banana: 2, orange: 1 }
```

---

## Khi nào nên dùng?

### ✅ Nên dùng Arrow Function

**1. Callback functions**

```javascript
// Event listeners
button.addEventListener('click', () => {
  console.log('Button clicked!');
});

// setTimeout/setInterval
setTimeout(() => console.log('Hello after 1s'), 1000);

// Array methods
const doubled = [1, 2, 3].map(x => x * 2);
```

**2. Promises và Async/Await**

```javascript
// Promises
fetch('/api/users')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Async/await
const getUsers = async () => {
  try {
    const response = await fetch('/api/users');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
};
```

**3. Khi cần kế thừa `this` từ bên ngoài**

```javascript
class Timer {
  constructor() {
    this.seconds = 0;
    
    // Arrow function kế thừa this từ constructor
    setInterval(() => {
      this.seconds++;
      console.log(this.seconds);
    }, 1000);
  }
}

const timer = new Timer(); // 1, 2, 3, 4, ...
```

### ❌ Không nên dùng Arrow Function

**1. Methods trong object (khi cần `this` riêng)**

```javascript
// ❌ Sai - this không trỏ đến person
const person = {
  name: 'Dũng',
  sayHi: () => {
    console.log('Xin chào, ' + this.name); // undefined
  }
};

// ✅ Đúng - dùng function thường
const person = {
  name: 'Dũng',
  sayHi: function() {
    console.log('Xin chào, ' + this.name); // Dũng
  }
};

// ✅ Hoặc dùng method shorthand (ES6)
const person = {
  name: 'Dũng',
  sayHi() {
    console.log('Xin chào, ' + this.name); // Dũng
  }
};
```

**2. Event handlers khi cần `this` là element**

```javascript
// ❌ Sai
button.addEventListener('click', () => {
  this.classList.add('active'); // this không phải button
});

// ✅ Đúng
button.addEventListener('click', function() {
  this.classList.add('active'); // this là button
});
```

**3. Constructors**

```javascript
// ❌ Sai - không thể dùng arrow function làm constructor
const Person = (name) => {
  this.name = name;
};

const person = new Person('Dũng'); // Error!

// ✅ Đúng - dùng function thường hoặc class
function Person(name) {
  this.name = name;
}

// Hoặc
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

---

## So sánh tổng hợp

| Tính năng | Function thường | Arrow Function |
|-----------|----------------|----------------|
| **Cú pháp** | `function() {}` | `() => {}` |
| **`this`** | Dynamic (tùy cách gọi) | Lexical (kế thừa) |
| **`arguments`** | Có object `arguments` | Không có |
| **Constructor** | Có thể dùng `new` | Không thể |
| **Implicit return** | Không | Có (khi 1 dòng) |
| **Hoisting** | Có | Không (với const/let) |

---

## Ví dụ thực tế

### 1. Xử lý danh sách sản phẩm

```javascript
const products = [
  { id: 1, name: 'Laptop', price: 20000000, inStock: true },
  { id: 2, name: 'Mouse', price: 200000, inStock: false },
  { id: 3, name: 'Keyboard', price: 500000, inStock: true },
  { id: 4, name: 'Monitor', price: 5000000, inStock: true }
];

// Lấy tên tất cả sản phẩm
const productNames = products.map(p => p.name);
console.log(productNames);
// ['Laptop', 'Mouse', 'Keyboard', 'Monitor']

// Lọc sản phẩm còn hàng
const availableProducts = products.filter(p => p.inStock);
console.log(availableProducts);
// [Laptop, Keyboard, Monitor]

// Tính tổng giá trị hàng tồn kho
const totalValue = products
  .filter(p => p.inStock)
  .reduce((sum, p) => sum + p.price, 0);
console.log(totalValue); // 25500000

// Tìm sản phẩm đắt nhất
const mostExpensive = products
  .reduce((max, p) => p.price > max.price ? p : max);
console.log(mostExpensive.name); // Laptop
```

### 2. Xử lý API với Async/Await

```javascript
// Fetch user data và posts
const getUserWithPosts = async (userId) => {
  try {
    // Lấy thông tin user
    const userResponse = await fetch(`/api/users/${userId}`);
    const user = await userResponse.json();
    
    // Lấy posts của user
    const postsResponse = await fetch(`/api/users/${userId}/posts`);
    const posts = await postsResponse.json();
    
    return {
      ...user,
      posts: posts
    };
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
};

// Sử dụng
getUserWithPosts(1)
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

### 3. Event handling trong Class

```javascript
class TodoApp {
  constructor() {
    this.todos = [];
    this.init();
  }
  
  init() {
    // Arrow function giữ this của class
    document.getElementById('add-btn').addEventListener('click', () => {
      this.addTodo();
    });
    
    document.getElementById('clear-btn').addEventListener('click', () => {
      this.clearAll();
    });
  }
  
  addTodo() {
    const input = document.getElementById('todo-input');
    if (input.value.trim()) {
      this.todos.push({
        id: Date.now(),
        text: input.value,
        completed: false
      });
      this.render();
      input.value = '';
    }
  }
  
  clearAll() {
    this.todos = [];
    this.render();
  }
  
  render() {
    const list = document.getElementById('todo-list');
    list.innerHTML = this.todos
      .map(todo => `<li>${todo.text}</li>`)
      .join('');
  }
}

const app = new TodoApp();
```

---

## Tips và Best Practices

### 1. Sử dụng parentheses cho rõ ràng

```javascript
// Có thể gây nhầm lẫn
const multiply = x => y => x * y;

// Rõ ràng hơn
const multiply = (x) => (y) => x * y;
```

### 2. Return object cần thêm ngoặc tròn

```javascript
// ❌ Sai - JavaScript nghĩ {} là block code
const createUser = (name, age) => { name: name, age: age };

// ✅ Đúng - thêm () để return object
const createUser = (name, age) => ({ name: name, age: age });

// Hoặc dùng shorthand
const createUser = (name, age) => ({ name, age });
```

### 3. Multiline arrow functions

```javascript
// Khi cần nhiều dòng, dùng {}
const processData = (data) => {
  const cleaned = data.filter(x => x !== null);
  const transformed = cleaned.map(x => x * 2);
  const result = transformed.reduce((sum, x) => sum + x, 0);
  return result;
};

// Hoặc chain methods
const processData = (data) => data
  .filter(x => x !== null)
  .map(x => x * 2)
  .reduce((sum, x) => sum + x, 0);
```

---

## Kết luận

Arrow function là một tính năng mạnh mẽ của ES6 giúp:

✅ **Code ngắn gọn hơn** - giảm boilerplate code  
✅ **Dễ đọc hơn** - cú pháp rõ ràng, đặc biệt với callbacks  
✅ **Ít bug hơn** - `this` predictable, không bị binding issues  
✅ **Hiện đại hơn** - là standard của JavaScript hiện nay  

**Quy tắc vàng:**
- Dùng arrow function cho **callbacks, array methods, promises**
- Dùng function thường cho **object methods, constructors, event handlers cần `this`**

Hãy thực hành nhiều để làm quen với arrow functions - chúng sẽ giúp code của bạn clean và professional hơn!

---

## Bài tập thực hành

Hãy thử viết lại các đoạn code sau bằng arrow function:

```javascript
// 1. Tính bình phương các số
const numbers = [1, 2, 3, 4, 5];
const squared = numbers.map(function(n) {
  return n * n;
});

// 2. Lọc số lẻ
const odds = numbers.filter(function(n) {
  return n % 2 !== 0;
});

// 3. Tìm user theo ID
function findUserById(users, id) {
  return users.find(function(user) {
    return user.id === id;
  });
}
```

**Đáp án:**

```javascript
// 1.
const squared = numbers.map(n => n * n);

// 2.
const odds = numbers.filter(n => n % 2 !== 0);

// 3.
const findUserById = (users, id) => users.find(user => user.id === id);
```

---

## Tài liệu tham khảo

- [MDN - Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [JavaScript.info - Arrow Functions Basics](https://javascript.info/arrow-functions-basics)
- [ES6 Features - Arrow Functions](http://es6-features.org/#ExpressionBodies)

---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">Tìm hiểu các kiến thức nền tảng về JavaScript - kiểu dữ liệu, OOP và functional programming</p>
    <div style="margin-top: 15px; display: flex; gap: 8px; flex-wrap: wrap;">
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">JavaScript</span>
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">OOP</span>
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">Functional</span>
    </div>
  </div>
</a>

<a href="/posts" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">📚</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Xem tất cả bài viết</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">Khám phá thêm nhiều bài viết về Java, JavaScript và lập trình</p>
  </div>
</a>

</div>