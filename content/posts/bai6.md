---
title: "JavaScript cơ bản"
date: 2025-10-10T05:00:00Z
draft: false
tags: ["JavaScript", "Programming", "Web Development"]
categories: ["JavaScript"]
author: "Nguyễn Tiến Dũng"
description: "Tìm hiểu các kiến thức nền tảng về JavaScript - kiểu dữ liệu, lập trình hướng đối tượng và functional programming"
summary: "JavaScript là ngôn ngữ lập trình phía client chạy trên trình duyệt. Các kiểu dữ liệu: Number, String, Boolean, Object, Array. JavaScript hỗ trợ lập trình hướng đối tượng và functional programming."
---

<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#javascript-là-gì">JavaScript là gì?</a></li>
    <li><a href="#các-kiểu-dữ-liệu-data-types">Các kiểu dữ liệu (Data Types)</a>
      <ul>
        <li><a href="#1-number">1. Number</a></li>
        <li><a href="#2-string">2. String</a></li>
        <li><a href="#3-boolean">3. Boolean</a></li>
        <li><a href="#4-object">4. Object</a></li>
        <li><a href="#5-array">5. Array</a></li>
        <li><a href="#6-undefined-và-null">6. Undefined và Null</a></li>
      </ul>
    </li>
    <li><a href="#biến-variables">Biến (Variables)</a></li>
    <li><a href="#lập-trình-hướng-đối-tượng-oop">Lập trình Hướng Đối Tượng (OOP)</a>
      <ul>
        <li><a href="#class-và-constructor">Class và Constructor</a></li>
        <li><a href="#kế-thừa-inheritance">Kế thừa (Inheritance)</a></li>
        <li><a href="#encapsulation-đóng-gói">Encapsulation (Đóng gói)</a></li>
      </ul>
    </li>
    <li><a href="#functional-programming">Functional Programming</a>
      <ul>
        <li><a href="#arrow-functions">Arrow Functions</a></li>
        <li><a href="#higher-order-functions">Higher-Order Functions</a></li>
        <li><a href="#pure-functions">Pure Functions</a></li>
        <li><a href="#immutability">Immutability</a></li>
      </ul>
    </li>
    <li><a href="#es6-features">ES6+ Features</a>
      <ul>
        <li><a href="#destructuring">Destructuring</a></li>
        <li><a href="#spread-operator">Spread Operator</a></li>
        <li><a href="#template-literals">Template Literals</a></li>
      </ul>
    </li>
    <li><a href="#ví-dụ-thực-tế">Ví dụ thực tế</a></li>
    <li><a href="#functional-programming-example">Functional Programming Example</a></li>
    <li><a href="#best-practices">Best Practices</a></li>
    <li><a href="#tổng-kết">Tổng kết</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## JavaScript là gì?

**JavaScript** là ngôn ngữ lập trình phía client chạy trên trình duyệt web. Được tạo ra bởi Brendan Eich năm 1995, JavaScript đã trở thành một trong ba công nghệ nền tảng của web development (HTML, CSS, JavaScript).

### Tại sao học JavaScript?

- **Phổ biến nhất**: Ngôn ngữ được sử dụng nhiều nhất thế giới
- **Chạy mọi nơi**: Browser, Server (Node.js), Mobile, Desktop
- **Cộng đồng lớn**: Hàng triệu developers và vô số thư viện
- **Cơ hội việc làm**: Nhu cầu tuyển dụng luôn cao

---

## Các kiểu dữ liệu (Data Types)

JavaScript có **8 kiểu dữ liệu**: 7 primitive và 1 complex.

### 1. Number (Số)
```javascript
let age = 25;
let price = 99.99;
let negative = -10;

// Phép toán
console.log(10 + 5);   // 15
console.log(10 - 5);   // 5
console.log(10 * 5);   // 50
console.log(10 / 5);   // 2
console.log(10 % 3);   // 1 (chia lấy dư)
console.log(2 ** 3);   // 8 (2 mũ 3)

// Math object
console.log(Math.round(4.7));   // 5
console.log(Math.random());     // số ngẫu nhiên 0-1
console.log(Math.max(1, 5, 3)); // 5
````

### 2. String (Chuỗi)
```javascript
let name = "John";
let greeting = 'Hello';

// Template literals (ES6)
let message = `My name is ${name}`;

// Các phương thức phổ biến
let text = "JavaScript";
console.log(text.length);          // 10
console.log(text.toLowerCase());   // "javascript"
console.log(text.includes("Script")); // true
console.log(text.slice(0, 4));     // "Java"
console.log(text.replace("Java", "Type")); // "TypeScript"

// Split & Join
let words = "Hello World".split(" ");  // ["Hello", "World"]
let joined = words.join("-");          // "Hello-World"
````

### 3. Boolean (Logic)
```javascript
let isActive = true;
let isLoggedIn = false;

// So sánh
console.log(5 > 3);       // true
console.log(10 === 10);   // true
console.log(5 !== 3);     // true

// Toán tử logic
console.log(true && false);  // false (AND)
console.log(true || false);  // true (OR)
console.log(!true);          // false (NOT)
````
### 4. Object (Đối tượng)
```javascript
let person = {
    name: "Nguyễn Văn A",
    age: 25,
    email: "email@gmail.com",
    greet: function() {
        console.log(`Xin chào, tôi là ${this.name}`);
    }
};

// Truy cập thuộc tính
console.log(person.name);  // "Nguyễn Văn A"
console.log(person["age"]); // 25

// Thêm/sửa/xóa
person.phone = "0123456789";
person.age = 26;
delete person.email;

person.greet();  // "Xin chào, tôi là Nguyễn Văn A"
````
### 5. Array (Mảng)
```javascript
let fruits = ["apple", "banana", "orange"];
let numbers = [1, 2, 3, 4, 5];
```
<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Sử dụng <code style="background: rgba(255,255,255,0.2); padding: 2px 6px; border-radius: 4px;">map</code>, <code style="background: rgba(255,255,255,0.2); padding: 2px 6px; border-radius: 4px;">filter</code>, <code style="background: rgba(255,255,255,0.2); padding: 2px 6px; border-radius: 4px;">reduce</code> thay vì for loops để code functional và dễ đọc hơn!</p>
</div>

```javascript
// Truy cập
console.log(fruits[0]);     // "apple"
console.log(fruits.length); // 3

// Thêm/xóa
fruits.push("grape");       // Thêm cuối
fruits.pop();               // Xóa cuối
fruits.unshift("mango");    // Thêm đầu
fruits.shift();             // Xóa đầu

// Các phương thức quan trọng
let arr = [1, 2, 3, 4, 5];

// map - Biến đổi
let doubled = arr.map(n => n * 2);  // [2, 4, 6, 8, 10]

// filter - Lọc
let evens = arr.filter(n => n % 2 === 0);  // [2, 4]

// reduce - Gộp
let sum = arr.reduce((total, n) => total + n, 0);  // 15

// find - Tìm
let found = arr.find(n => n > 3);  // 4

// includes - Kiểm tra
console.log(arr.includes(3));  // true
````
### 6. Undefined và Null
```javascript
let x;                    // undefined
let user = null;          // null

console.log(x);           // undefined
console.log(user);        // null
console.log(undefined == null);   // true
console.log(undefined === null);  // false
````
### Biến (Variables)
JavaScript có 3 cách khai báo biến:
```javascript
// var (cũ, không khuyến khích)
var name = "John";

// let (ES6, có thể thay đổi)
let age = 30;
age = 31;  // OK

// const (ES6, không thay đổi)
const PI = 3.14;
// PI = 3.14159;  // ❌ Error!

// Với object/array
const person = {name: "John"};
person.name = "Jane";  // ✅ OK (thay đổi thuộc tính)
// person = {};        // ❌ Error! (không thể gán lại)
````
### Lập trình Hướng Đối Tượng (OOP)
Class và Constructor
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        console.log(`Xin chào, tôi là ${this.name}`);
    }
    
    haveBirthday() {
        this.age++;
    }
}

// Tạo instance
let person1 = new Person("An", 25);
person1.greet();         // "Xin chào, tôi là An"
person1.haveBirthday();
console.log(person1.age); // 26
````
### Kế thừa (Inheritance)
```javascript
class Student extends Person {
    constructor(name, age, school) {
        super(name, age);  // Gọi constructor cha
        this.school = school;
    }
    
    study() {
        console.log(`${this.name} đang học tại ${this.school}`);
    }
}

let student = new Student("Lan", 16, "THPT Chu Văn An");
student.greet();   // Kế thừa từ Person
student.study();   // "Lan đang học tại THPT Chu Văn An"
````
### Encapsulation (Đóng gói)
```javascript
class BankAccount {
    #balance = 0;  // Private field
    
    constructor(owner, balance) {
        this.owner = owner;
        this.#balance = balance;
    }
    
    deposit(amount) {
        this.#balance += amount;
        console.log(`Số dư: ${this.#balance}đ`);
    }
    
    withdraw(amount) {
        if (amount > this.#balance) {
            console.log("Số dư không đủ!");
            return;
        }
        this.#balance -= amount;
        console.log(`Số dư: ${this.#balance}đ`);
    }
    
    getBalance() {
        return this.#balance;
    }
}

let account = new BankAccount("Nguyễn Văn A", 1000000);
account.deposit(500000);   // "Số dư: 1500000đ"
account.withdraw(200000);  // "Số dư: 1300000đ"
````
<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;">Private fields (#balance) chỉ hoạt động trong môi trường hỗ trợ ES2022+. Với các version cũ hơn, sử dụng WeakMap hoặc closure để đạt được encapsulation.</p>
</div>

### Functional Programming
JavaScript hỗ trợ lập trình hàm với các tính năng:
### Arrow Functions
```javascript
// Function thường
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// 1 tham số
const square = x => x * x;

// Nhiều dòng
const greet = name => {
    const message = `Hello ${name}`;
    return message;
};
````
### Higher-Order Functions
```javascript
let numbers = [1, 2, 3, 4, 5];

// map - Biến đổi từng phần tử
let doubled = numbers.map(n => n * 2);
console.log(doubled);  // [2, 4, 6, 8, 10]

// filter - Lọc theo điều kiện
let evens = numbers.filter(n => n % 2 === 0);
console.log(evens);  // [2, 4]

// reduce - Gộp thành 1 giá trị
let sum = numbers.reduce((total, n) => total + n, 0);
console.log(sum);  // 15

// Kết hợp các phương thức
let result = numbers
    .filter(n => n > 2)
    .map(n => n * 2)
    .reduce((sum, n) => sum + n, 0);
console.log(result);  // 24
````
### Pure Functions
```javascript
// ✅ Pure function - Luôn trả về cùng kết quả
function add(a, b) {
    return a + b;
}

// ❌ Impure function - Phụ thuộc biến ngoài
let total = 0;
function addToTotal(value) {
    total += value;  // Side effect
    return total;
}
````
### Immutability
```javascript
// ❌ Mutable - Thay đổi mảng gốc
let arr = [1, 2, 3];
arr.push(4);

// ✅ Immutable - Tạo mảng mới
let arr = [1, 2, 3];
let newArr = [...arr, 4];

// Object
let user = {name: "John", age: 30};
let updated = {...user, age: 31};  // Tạo object mới
````
### ES6+ Features
### Destructuring
```javascript
// Array
let [a, b, c] = [1, 2, 3];
console.log(a);  // 1

// Object
let person = {name: "John", age: 30};
let {name, age} = person;
console.log(name);  // "John"

// Function parameters
function greet({name, age}) {
    console.log(`Hello ${name}, ${age} years old`);
}
````
### Spread Operator
```javascript
// Array
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];  // [1, 2, 3, 4, 5]

// Object
let user = {name: "John", age: 30};
let updated = {...user, age: 31};  // {name: "John", age: 31}

// Function
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}
console.log(sum(1, 2, 3, 4));  // 10
````
### Template Literals
```javascript
let name = "John";
let age = 30;

let message = `My name is ${name} and I am ${age} years old`;
console.log(message);

// Multi-line
let html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;
````
### Ví dụ thực tế
### Todo List với OOP
```javascript
class TodoList {
    constructor() {
        this.todos = [];
    }
    
    addTodo(text) {
        this.todos.push({
            id: Date.now(),
            text: text,
            completed: false
        });
    }
    
    removeTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id);
    }
    
    toggleTodo(id) {
        this.todos = this.todos.map(todo =>
            todo.id === id ? {...todo, completed: !todo.completed} : todo
        );
    }
    
    getAll() {
        return this.todos;
    }
    
    getCompleted() {
        return this.todos.filter(todo => todo.completed);
    }
}

// Sử dụng
let todoList = new TodoList();
todoList.addTodo("Học JavaScript");
todoList.addTodo("Làm bài tập");
todoList.toggleTodo(1);
console.log(todoList.getAll());
````
### Functional Programming Example
```javascript
// Quản lý danh sách sinh viên
let students = [
    {name: "An", score: 85},
    {name: "Bình", score: 92},
    {name: "Chi", score: 78},
    {name: "Dũng", score: 95}
];

// Lấy tên sinh viên điểm > 80
let goodStudents = students
    .filter(s => s.score > 80)
    .map(s => s.name);

console.log(goodStudents);  // ["An", "Bình", "Dũng"]

// Tính điểm trung bình
let avgScore = students
    .map(s => s.score)
    .reduce((sum, score) => sum + score, 0) / students.length;

console.log(avgScore);  // 87.5
````
### Best Practices
1. Sử dụng const và let thay vì var
```javascript
// ✅ Tốt
const PI = 3.14;
let count = 0;

// ❌ Tránh
var x = 10;
````
2. Sử dụng === thay vì ==
```javascript
// ✅ Tốt - So sánh cả kiểu
console.log(5 === 5);      // true
console.log(5 === "5");    // false

// ❌ Tránh - Chỉ so sánh giá trị
console.log(5 == "5");     // true (confusing!)
````
<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Lỗi thường gặp</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;"><strong>Type coercion với ==:</strong> <code>0 == ""</code> trả về <code>true</code>, <code>null == undefined</code> trả về <code>true</code>. Điều này gây confusing! Luôn dùng <code>===</code> để tránh bugs.</p>
</div>

3. Sử dụng Arrow Functions
```javascript
// ✅ Tốt - Ngắn gọn
const double = x => x * 2;
arr.map(n => n * 2);

// ❌ Dài dòng
function double(x) {
    return x * 2;
}
arr.map(function(n) {
    return n * 2;
});
````
4. Immutability
```javascript
// ✅ Tốt - Không thay đổi gốc
let newArr = [...arr, 4];
let newObj = {...obj, age: 31};

// ❌ Tránh - Thay đổi gốc
arr.push(4);
obj.age = 31;
````
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Immutability giúp tránh side effects, dễ debug hơn, và là requirement cho React/Redux. Code sẽ predictable và ít bugs hơn.</p>
</div>

### Tổng kết
JavaScript là ngôn ngữ linh hoạt, hỗ trợ nhiều paradigm:
#### Kiến thức cốt lõi:

Các kiểu dữ liệu: Number, String, Boolean, Object, Array

Biến: const, let (tránh var)

OOP: Class, Inheritance, Encapsulation

Functional: Arrow functions, map/filter/reduce

ES6+: Destructuring, Spread, Template literals
## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** Sự khác biệt giữa `let`, `const` và `var` là gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <ul style="margin: 0;">
      <li><code>var</code>: Function-scoped, có hoisting, có thể redeclare</li>
      <li><code>let</code>: Block-scoped, không có hoisting, có thể reassign</li>
      <li><code>const</code>: Block-scoped, không có hoisting, không thể reassign</li>
    </ul>
    <p style="margin: 10px 0 0 0;"><strong>Khuyên dùng:</strong> <code>const</code> by default, <code>let</code> khi cần thay đổi, tránh <code>var</code></p>
  </div>
</details>

**Câu 2:** `map()` và `forEach()` khác nhau như thế nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong><code>map()</code>:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Trả về array mới</li>
      <li>✅ Không thay đổi array gốc</li>
      <li>✅ Dùng để transform data</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong><code>forEach()</code>:</strong></p>
    <ul style="margin: 0;">
      <li>❌ Trả về <code>undefined</code></li>
      <li>✅ Dùng cho side effects (console.log, update DOM)</li>
    </ul>
  </div>
</details>

**Câu 3:** Arrow function và function thường khác nhau về `this` như thế nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Function thường:</strong> <code>this</code> dynamic, phụ thuộc cách gọi</p>
    <p style="margin: 0 0 10px 0;"><strong>Arrow function:</strong> <code>this</code> lexical, kế thừa từ outer scope</p>
    <p style="margin: 10px 0 0 0;"><strong>→</strong> Arrow function không có <code>this</code> riêng!</p>
  </div>
</details>

**Câu 4:** Khi nào dùng `reduce()` thay vì `map()` hoặc `filter()`?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0;">Dùng <code>reduce()</code> khi cần:</p>
    <ul style="margin: 10px 0 0 0;">
      <li>Gộp array thành 1 giá trị (sum, max, min)</li>
      <li>Transform array thành object</li>
      <li>Flatten nested arrays</li>
      <li>Group data by property</li>
    </ul>
  </div>
</details>

**Câu 5:** Immutability là gì và tại sao quan trọng?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Immutability:</strong> Không thay đổi data gốc, tạo copy mới thay vì modify</p>
    <p style="margin: 0 0 10px 0;"><strong>Lợi ích:</strong></p>
    <ul style="margin: 0;">
      <li>✅ Tránh side effects và bugs</li>
      <li>✅ Dễ debug (data predictable)</li>
      <li>✅ Required cho React/Redux</li>
      <li>✅ Dễ test và maintain</li>
    </ul>
  </div>
</details>

</div>

### Bài tập thực hành

### Bài 1: Tính tổng mảng
```javascript
// Viết hàm tính tổng các số trong mảng
function sum(arr) {
    // Your code here
}

console.log(sum([1, 2, 3, 4, 5]));  // 15
````
### Đáp án
```
Bài 1
const sum = arr => arr.reduce((total, n) => total + n, 0);
````
### Bài 2: Lọc số chẵn
```javascript
// Viết hàm lọc số chẵn
function filterEven(arr) {
    // Your code here
}

console.log(filterEven([1, 2, 3, 4, 5, 6]));  // [2, 4, 6]
````
### Đáp án
```
Bài 2
const filterEven = arr => arr.filter(n => n % 2 === 0);
````
### Bài 3: Class Student
```javascript
// Tạo class Student với name, age
// Method: introduce() - in ra "My name is X, I am Y years old"

// Your code here

let student = new Student("An", 16);
student.introduce();  // "My name is An, I am 16 years old"
````
### Đáp án
```
Bài 3
class Student {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    introduce() {
        console.log(`My name is ${this.name}, I am ${this.age} years old`);
    }
}
````
### Tài liệu tham khảo

MDN JavaScript Guide

JavaScript.info

W3Schools JavaScript

---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai9" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px;">➡️</div>
    <h4 style="margin: 0 0 10px 0; color: #333; font-size: 20px;">Arrow Functions & ES6</h4>
    <p style="margin: 0; color: #666; font-size: 14px; line-height: 1.6;">Tìm hiểu về Arrow Functions trong ES6 - cú pháp ngắn gọn, this binding và cách sử dụng hiệu quả</p>
    <div style="margin-top: 15px; display: flex; gap: 8px; flex-wrap: wrap;">
      <span style="background: rgba(255,255,255,0.7); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: #333;">JavaScript</span>
      <span style="background: rgba(255,255,255,0.7); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: #333;">ES6</span>
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











