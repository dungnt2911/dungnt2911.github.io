---
title: "DOM Manipulation - Thao tác với DOM trong JavaScript"
date: 2025-10-10T06:00:00Z
draft: false
tags: ["JavaScript", "DOM", "Web Development"]
categories: ["JavaScript"]
author: "Nguyễn Tiến Dũng"
description: "Tìm hiểu cách thao tác với DOM - thay đổi nội dung, thuộc tính, CSS và xử lý events trong JavaScript"
summary: "DOM (Document Object Model) là cấu trúc cây của trang web. JavaScript có thể thay đổi nội dung, thuộc tính và CSS của phần tử HTML."
---
<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#dom-là-gì">DOM là gì?</a></li>
    <li><a href="#selecting-elements-chọn-phần-tử">Selecting Elements (Chọn phần tử)</a></li>
    <li><a href="#thay-đổi-nội-dung-content">Thay đổi nội dung (Content)</a></li>
    <li><a href="#thay-đổi-thuộc-tính-attributes">Thay đổi thuộc tính (Attributes)</a></li>
    <li><a href="#thay-đổi-style-css">Thay đổi Style (CSS)</a></li>
    <li><a href="#tạo-và-xóa-elements">Tạo và xóa Elements</a></li>
    <li><a href="#event-handling">Event Handling</a></li>
    <li><a href="#traversing-dom-di-chuyển-trong-dom">Traversing DOM (Di chuyển trong DOM)</a></li>
    <li><a href="#ví-dụ-thực-tế">Ví dụ thực tế</a></li>
    <li><a href="#best-practices">Best Practices</a></li>
    <li><a href="#performance-tips">Performance Tips</a></li>
    <li><a href="#common-mistakes">Common Mistakes</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## DOM là gì?

**DOM (Document Object Model)** là giao diện lập trình cho HTML và XML documents. Nó biểu diễn trang web dưới dạng **cây cấu trúc** (tree structure), trong đó:

- Mỗi element HTML là một **node**
- Các node có quan hệ cha-con (parent-child)
- JavaScript có thể truy cập và thay đổi mọi node trong cây DOM

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">DOM là <strong>cầu nối giữa JavaScript và HTML</strong>! Mọi thứ trong webpage (tags, text, attributes) đều là DOM nodes. Hiểu DOM tree structure giúp bạn manipulate bất kỳ element nào trên page - từ thay đổi text, style, đến tạo/xóa elements. Đây là <strong>foundation của interactive web development</strong>!</p>
</div>

### Cấu trúc DOM Tree

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a paragraph</p>
  </body>
</html>
```

Cây DOM:

```
Document
  └── html
       ├── head
       │    └── title
       │         └── "My Page"
       └── body
            ├── h1
            │    └── "Hello World"
            └── p
                 └── "This is a paragraph"
```

---

## Selecting Elements (Chọn phần tử)

### 1. getElementById()

Chọn element theo **ID** (duy nhất).

```html
<h1 id="title">Hello</h1>
<button id="btn">Click me</button>
```

```javascript
// Lấy element bằng ID
const title = document.getElementById('title');
console.log(title); // <h1 id="title">Hello</h1>

const button = document.getElementById('btn');
console.log(button.textContent); // "Click me"
```

### 2. getElementsByClassName()

Chọn **tất cả** elements có class name (trả về HTMLCollection).

```html
<p class="text">Paragraph 1</p>
<p class="text">Paragraph 2</p>
<p class="text">Paragraph 3</p>
```

```javascript
// Lấy tất cả elements có class "text"
const paragraphs = document.getElementsByClassName('text');
console.log(paragraphs.length); // 3

// Duyệt qua các elements
for (let i = 0; i < paragraphs.length; i++) {
  console.log(paragraphs[i].textContent);
}
// Output:
// Paragraph 1
// Paragraph 2
// Paragraph 3
```

### 3. getElementsByTagName()

Chọn **tất cả** elements theo tag name.

```html
<div>Div 1</div>
<div>Div 2</div>
<p>Paragraph</p>
```

```javascript
// Lấy tất cả thẻ div
const divs = document.getElementsByTagName('div');
console.log(divs.length); // 2

// Lấy tất cả thẻ p
const paragraphs = document.getElementsByTagName('p');
console.log(paragraphs.length); // 1
```

### 4. querySelector() - KHUYẾN NGHỊ

Chọn **element đầu tiên** khớp với CSS selector.

```html
<div class="container">
  <h1 class="title">Main Title</h1>
  <p class="text">First paragraph</p>
  <p class="text">Second paragraph</p>
</div>
```

```javascript
// Chọn element đầu tiên có class "text"
const firstPara = document.querySelector('.text');
console.log(firstPara.textContent); // "First paragraph"

// Chọn h1 trong .container
const title = document.querySelector('.container .title');
console.log(title.textContent); // "Main Title"

// Chọn theo attribute
const input = document.querySelector('input[type="email"]');

// Chọn theo pseudo-class
const firstChild = document.querySelector('li:first-child');
```
<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>querySelector() trả về NULL nếu không tìm thấy element!</strong> Nếu gọi method trên null → <code>TypeError: Cannot read property of null</code>. Luôn check <code>if (element)</code> trước khi manipulate, đặc biệt khi script chạy trước khi DOM load xong. Hoặc dùng <code>DOMContentLoaded</code> event!</p>
</div>

### 5. QuerySelectorAll()

Chọn **tất cả** elements khớp với CSS selector (trả về NodeList).

```html
<ul>
  <li class="item">Item 1</li>
  <li class="item">Item 2</li>
  <li class="item">Item 3</li>
</ul>
```

```javascript
// Lấy tất cả li có class "item"
const items = document.querySelectorAll('.item');
console.log(items.length); // 3

// Duyệt bằng forEach (NodeList hỗ trợ forEach)
items.forEach((item, index) => {
  console.log(`${index}: ${item.textContent}`);
});
// Output:
// 0: Item 1
// 1: Item 2
// 2: Item 3
```

---

## Thay đổi nội dung (Content)

### textContent vs innerHTML

```html
<div id="content">
  <p>Hello <strong>World</strong></p>
</div>
```

```javascript
const div = document.getElementById('content');

// textContent - Chỉ lấy text thuần
console.log(div.textContent); // "Hello World"

// innerHTML - Lấy cả HTML tags
console.log(div.innerHTML); // "<p>Hello <strong>World</strong></p>"

// Thay đổi textContent
div.textContent = 'New text';
// Result: <div id="content">New text</div>

// Thay đổi innerHTML
div.innerHTML = '<h1>New HTML</h1>';
// Result: <div id="content"><h1>New HTML</h1></div>
```

### innerText vs textContent

```javascript
const element = document.getElementById('example');

// textContent - Lấy tất cả text, kể cả ẩn
console.log(element.textContent);

// innerText - Chỉ lấy text hiển thị (giống user nhìn thấy)
console.log(element.innerText);
```

---

## Thay đổi thuộc tính (Attributes)

### getAttribute() & setAttribute()

```html
<img id="photo" src="old.jpg" alt="Old photo">
<a id="link" href="https://old.com">Link</a>
```

```javascript
const img = document.getElementById('photo');
const link = document.getElementById('link');

// Lấy attribute
console.log(img.getAttribute('src')); // "old.jpg"
console.log(link.getAttribute('href')); // "https://old.com"

// Thay đổi attribute
img.setAttribute('src', 'new.jpg');
img.setAttribute('alt', 'New photo');

link.setAttribute('href', 'https://google.com');
link.setAttribute('target', '_blank');
```

### Truy cập trực tiếp

```javascript
const img = document.getElementById('photo');

// Đọc attribute
console.log(img.src);  // "old.jpg"
console.log(img.alt);  // "Old photo"

// Thay đổi attribute
img.src = 'new.jpg';
img.alt = 'New photo';

// Với links
const link = document.getElementById('link');
link.href = 'https://facebook.com';
link.target = '_blank';

// Với inputs
const input = document.querySelector('input');
input.value = 'New value';
input.placeholder = 'Enter text';
input.disabled = true;
```

---

## Thay đổi Style (CSS)

### style property

```html
<div id="box">Box</div>
```

```javascript
const box = document.getElementById('box');

// Thay đổi từng property
box.style.color = 'red';
box.style.backgroundColor = 'yellow';
box.style.fontSize = '20px';
box.style.padding = '10px';
box.style.border = '2px solid black';

// Lưu ý: CSS property dùng camelCase
// background-color → backgroundColor
// font-size → fontSize
// border-radius → borderRadius
```

### classList - KHUYẾN NGHỊ

```html
<style>
  .active { background: green; color: white; }
  .large { font-size: 24px; }
  .hidden { display: none; }
</style>

<div id="box" class="box">Box</div>
```

```javascript
const box = document.getElementById('box');

// Thêm class
box.classList.add('active');
box.classList.add('large');

// Xóa class
box.classList.remove('large');

// Toggle class (có thì xóa, không có thì thêm)
box.classList.toggle('hidden');

// Kiểm tra có class không
if (box.classList.contains('active')) {
  console.log('Box is active');
}

// Thay thế class
box.classList.replace('active', 'inactive');
```

---

## Tạo và xóa Elements

### createElement() & appendChild()

```javascript
// Tạo element mới
const newDiv = document.createElement('div');
newDiv.textContent = 'I am a new div';
newDiv.classList.add('new-class');

// Thêm vào DOM
document.body.appendChild(newDiv);

// Ví dụ phức tạp hơn
const card = document.createElement('div');
card.className = 'card';

const title = document.createElement('h2');
title.textContent = 'Card Title';

const content = document.createElement('p');
content.textContent = 'Card content here';

card.appendChild(title);
card.appendChild(content);

document.body.appendChild(card);
```

### insertBefore() & insertAdjacentHTML()

```html
<ul id="list">
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```javascript
const list = document.getElementById('list');

// insertBefore - Chèn trước một element
const newItem = document.createElement('li');
newItem.textContent = 'Item 1';

const firstItem = list.firstElementChild;
list.insertBefore(newItem, firstItem);

// insertAdjacentHTML - Chèn HTML
list.insertAdjacentHTML('beforeend', '<li>Item 4</li>');
list.insertAdjacentHTML('afterbegin', '<li>Item 0</li>');
```

### removeChild() & remove()

```javascript
// Cách 1: removeChild (cần biết parent)
const parent = document.getElementById('parent');
const child = document.getElementById('child');
parent.removeChild(child);

// Cách 2: remove (dễ hơn)
const element = document.getElementById('element');
element.remove();
```

---

## Event Handling

### addEventListener()

```html
<button id="btn">Click me</button>
<input type="text" id="input">
```

```javascript
const button = document.getElementById('btn');

// Click event
button.addEventListener('click', function() {
  console.log('Button clicked!');
});

// Với arrow function
button.addEventListener('click', () => {
  console.log('Button clicked!');
});

// Input events
const input = document.getElementById('input');

input.addEventListener('input', (e) => {
  console.log('Value:', e.target.value);
});

input.addEventListener('focus', () => {
  console.log('Input focused');
});

input.addEventListener('blur', () => {
  console.log('Input lost focus');
});
```
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Luôn dùng <code>addEventListener()</code> thay vì inline events (<code>onclick</code>) hoặc <code>element.onclick</code>. addEventListener cho phép <strong>multiple handlers</strong> cho cùng 1 event, dễ remove listener, và tách biệt JS khỏi HTML. Code sẽ maintainable và scalable hơn nhiều!</p>
</div>

### Event object

```javascript
button.addEventListener('click', (event) => {
  console.log('Event type:', event.type);        // "click"
  console.log('Target:', event.target);          // <button>
  console.log('Current target:', event.currentTarget);
  
  // Prevent default behavior
  event.preventDefault();
  
  // Stop propagation
  event.stopPropagation();
});
```

### Common Events

```javascript
// Mouse events
element.addEventListener('click', handler);
element.addEventListener('dblclick', handler);
element.addEventListener('mouseenter', handler);
element.addEventListener('mouseleave', handler);
element.addEventListener('mousemove', handler);

// Keyboard events
document.addEventListener('keydown', handler);
document.addEventListener('keyup', handler);
document.addEventListener('keypress', handler);

// Form events
form.addEventListener('submit', handler);
input.addEventListener('change', handler);
input.addEventListener('input', handler);
input.addEventListener('focus', handler);
input.addEventListener('blur', handler);

// Window events
window.addEventListener('load', handler);
window.addEventListener('resize', handler);
window.addEventListener('scroll', handler);
```

---

## Traversing DOM (Di chuyển trong DOM)

### Parent, Children, Siblings

```html
<div id="parent">
  <div id="child1">Child 1</div>
  <div id="child2">Child 2</div>
  <div id="child3">Child 3</div>
</div>
```

```javascript
const child2 = document.getElementById('child2');

// Parent
console.log(child2.parentElement);           // <div id="parent">
console.log(child2.parentNode);              // <div id="parent">

// Children
const parent = document.getElementById('parent');
console.log(parent.children);                // HTMLCollection [div, div, div]
console.log(parent.firstElementChild);       // <div id="child1">
console.log(parent.lastElementChild);        // <div id="child3">

// Siblings
console.log(child2.previousElementSibling);  // <div id="child1">
console.log(child2.nextElementSibling);      // <div id="child3">
```

---

## Ví dụ thực tế

### 1. Todo List

```html
<!DOCTYPE html>
<html>
<head>
  <title>Todo List</title>
  <style>
    .todo-item { padding: 10px; border-bottom: 1px solid #ddd; }
    .completed { text-decoration: line-through; color: gray; }
  </style>
</head>
<body>
  <h1>My Todo List</h1>
  <input type="text" id="todoInput" placeholder="Enter todo...">
  <button id="addBtn">Add</button>
  <ul id="todoList"></ul>

  <script>
    const input = document.getElementById('todoInput');
    const addBtn = document.getElementById('addBtn');
    const todoList = document.getElementById('todoList');

    addBtn.addEventListener('click', addTodo);
    input.addEventListener('keypress', (e) => {
      if (e.key === 'Enter') addTodo();
    });

    function addTodo() {
      const text = input.value.trim();
      if (text === '') return;

      // Tạo todo item
      const li = document.createElement('li');
      li.className = 'todo-item';
      
      const span = document.createElement('span');
      span.textContent = text;
      span.addEventListener('click', function() {
        this.parentElement.classList.toggle('completed');
      });
      
      const deleteBtn = document.createElement('button');
      deleteBtn.textContent = 'Delete';
      deleteBtn.addEventListener('click', function() {
        this.parentElement.remove();
      });
      
      li.appendChild(span);
      li.appendChild(deleteBtn);
      todoList.appendChild(li);
      
      input.value = '';
    }
  </script>
</body>
</html>
```

### 2. Counter App

```html
<!DOCTYPE html>
<html>
<head>
  <title>Counter</title>
  <style>
    #counter { font-size: 48px; text-align: center; margin: 20px; }
    button { font-size: 20px; margin: 5px; padding: 10px 20px; }
  </style>
</head>
<body>
  <div id="counter">0</div>
  <button id="decreaseBtn">-</button>
  <button id="resetBtn">Reset</button>
  <button id="increaseBtn">+</button>

  <script>
    let count = 0;
    const counterDisplay = document.getElementById('counter');
    const decreaseBtn = document.getElementById('decreaseBtn');
    const resetBtn = document.getElementById('resetBtn');
    const increaseBtn = document.getElementById('increaseBtn');

    function updateDisplay() {
      counterDisplay.textContent = count;
      
      // Change color based on value
      if (count > 0) {
        counterDisplay.style.color = 'green';
      } else if (count < 0) {
        counterDisplay.style.color = 'red';
      } else {
        counterDisplay.style.color = 'black';
      }
    }

    increaseBtn.addEventListener('click', () => {
      count++;
      updateDisplay();
    });

    decreaseBtn.addEventListener('click', () => {
      count--;
      updateDisplay();
    });

    resetBtn.addEventListener('click', () => {
      count = 0;
      updateDisplay();
    });
  </script>
</body>
</html>
```

### 3. Image Gallery

```html
<!DOCTYPE html>
<html>
<head>
  <title>Image Gallery</title>
  <style>
    .gallery { display: flex; gap: 10px; flex-wrap: wrap; }
    .gallery img { width: 200px; height: 200px; object-fit: cover; cursor: pointer; }
    .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); justify-content: center; align-items: center; }
    .modal img { max-width: 90%; max-height: 90%; }
    .modal.active { display: flex; }
  </style>
</head>
<body>
  <div class="gallery" id="gallery"></div>
  <div class="modal" id="modal">
    <img id="modalImage" src="">
  </div>

  <script>
    const images = [
      'https://picsum.photos/200/200?random=1',
      'https://picsum.photos/200/200?random=2',
      'https://picsum.photos/200/200?random=3',
      'https://picsum.photos/200/200?random=4',
      'https://picsum.photos/200/200?random=5',
      'https://picsum.photos/200/200?random=6'
    ];

    const gallery = document.getElementById('gallery');
    const modal = document.getElementById('modal');
    const modalImage = document.getElementById('modalImage');

    // Tạo gallery
    images.forEach(src => {
      const img = document.createElement('img');
      img.src = src;
      img.addEventListener('click', () => {
        modalImage.src = src;
        modal.classList.add('active');
      });
      gallery.appendChild(img);
    });

    // Đóng modal khi click
    modal.addEventListener('click', () => {
      modal.classList.remove('active');
    });
  </script>
</body>
</html>
```

---

## Best Practices

### 1. Cache DOM references

```javascript
// ❌ Không tốt - Query nhiều lần
function updateList() {
  document.getElementById('list').innerHTML = '';
  document.getElementById('list').appendChild(item1);
  document.getElementById('list').appendChild(item2);
}

// ✅ Tốt - Cache reference
function updateList() {
  const list = document.getElementById('list');
  list.innerHTML = '';
  list.appendChild(item1);
  list.appendChild(item2);
}
```

### 2. Event Delegation

```javascript
// ❌ Không tốt - Gắn event cho từng item
items.forEach(item => {
  item.addEventListener('click', handleClick);
});

// ✅ Tốt - Event delegation
const list = document.getElementById('list');
list.addEventListener('click', (e) => {
  if (e.target.classList.contains('item')) {
    handleClick(e);
  }
});
```

### 3. Minimize reflows/repaints

```javascript
// ❌ Không tốt - Nhiều reflows
element.style.width = '100px';
element.style.height = '100px';
element.style.backgroundColor = 'red';

// ✅ Tốt - 1 reflow
element.style.cssText = 'width: 100px; height: 100px; background-color: red;';

// Hoặc dùng class
element.classList.add('styled');
```

---

## Performance Tips

### 1. DocumentFragment

```javascript
// ❌ Chậm - Thêm từng element
const list = document.getElementById('list');
for (let i = 0; i < 1000; i++) {
  const li = document.createElement('li');
  li.textContent = `Item ${i}`;
  list.appendChild(li); // Reflow mỗi lần
}

// ✅ Nhanh - Dùng DocumentFragment
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const li = document.createElement('li');
  li.textContent = `Item ${i}`;
  fragment.appendChild(li);
}
list.appendChild(fragment); // Chỉ 1 reflow
```

### 2. innerHTML vs createElement

```javascript
// Nhanh hơn cho nhiều elements
container.innerHTML = `
  <div class="card">
    <h2>Title</h2>
    <p>Content</p>
  </div>
`;

// An toàn hơn, có control tốt hơn
const card = document.createElement('div');
card.className = 'card';
// ...
container.appendChild(card);
```

---

## Common Mistakes

### 1. Quên check null

```javascript
// ❌ Sai - Element có thể null
const element = document.getElementById('notExist');
element.style.color = 'red'; // Error!

// ✅ Đúng - Check trước
const element = document.getElementById('notExist');
if (element) {
  element.style.color = 'red';
}
```

### 2. Timing issues

```javascript
// ❌ Sai - DOM chưa load xong
const button = document.getElementById('btn');
button.addEventListener('click', handler);

// ✅ Đúng - Đợi DOM ready
document.addEventListener('DOMContentLoaded', () => {
  const button = document.getElementById('btn');
  button.addEventListener('click', handler);
});
```
---

## 🐛 Lỗi thường gặp với DOM Manipulation

### ❌ Lỗi 1: Manipulate element trước khi DOM load xong

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Cannot read property of null</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Script chạy trước khi HTML parse xong → elements chưa tồn tại → <code>querySelector()</code> trả về <code>null</code>!</p>
</div>

**Ví dụ SAI:**
```html
<!-- ❌ SAI - Script trong <head> -->
<!DOCTYPE html>
<html>
<head>
    <script>
        // DOM chưa load xong!
        const button = document.querySelector('#myButton');
        button.addEventListener('click', () => {
            console.log('Clicked');
        }); // ❌ Error: Cannot read property 'addEventListener' of null
    </script>
</head>
<body>
    <button id="myButton">Click me</button>
</body>
</html>
```

**Lỗi:**
```
TypeError: Cannot read property 'addEventListener' of null
```

**Cách fix:**
```html
<!-- ✅ ĐÚNG - Cách 1: Script ở cuối body -->
<!DOCTYPE html>
<html>
<head></head>
<body>
    <button id="myButton">Click me</button>
    
    <script>
        // DOM đã load xong!
        const button = document.querySelector('#myButton');
        button.addEventListener('click', () => {
            console.log('Clicked');
        }); // ✅ OK
    </script>
</body>
</html>

<!-- ✅ ĐÚNG - Cách 2: DOMContentLoaded event -->
<!DOCTYPE html>
<html>
<head>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Chỉ chạy sau khi DOM ready!
            const button = document.querySelector('#myButton');
            button.addEventListener('click', () => {
                console.log('Clicked');
            }); // ✅ OK
        });
    </script>
</head>
<body>
    <button id="myButton">Click me</button>
</body>
</html>

<!-- ✅ ĐÚNG - Cách 3: defer attribute -->
<!DOCTYPE html>
<html>
<head>
    <script src="app.js" defer></script>
    <!-- defer: load song song, execute sau khi DOM ready -->
</head>
<body>
    <button id="myButton">Click me</button>
</body>
</html>
```

---

### ❌ Lỗi 2: innerHTML với user input → XSS vulnerability

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Cross-Site Scripting (XSS)</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Dùng <code>innerHTML</code> với user input không sanitize → attacker có thể inject malicious script!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ NGUY HIỂM - Dễ bị XSS attack!
const userInput = prompt("Enter your name:");
document.getElementById('greeting').innerHTML = 
    `<h1>Hello, ${userInput}!</h1>`;

// Nếu user nhập: <img src=x onerror="alert('Hacked!')">
// → Script sẽ execute! 💀
```

**Attacker input:**
```html
<img src=x onerror="alert('XSS Attack!')">
<script>document.cookie</script>
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Cách 1: Dùng textContent (escape HTML)
const userInput = prompt("Enter your name:");
const h1 = document.createElement('h1');
h1.textContent = `Hello, ${userInput}!`; // Escape HTML tự động
document.getElementById('greeting').appendChild(h1);

// ✅ ĐÚNG - Cách 2: Sanitize input
function sanitizeHTML(str) {
    const temp = document.createElement('div');
    temp.textContent = str;
    return temp.innerHTML;
}

const safe = sanitizeHTML(userInput);
document.getElementById('greeting').innerHTML = 
    `<h1>Hello, ${safe}!</h1>`;

// ✅ ĐÚNG - Cách 3: Dùng library (DOMPurify)
import DOMPurify from 'dompurify';
const clean = DOMPurify.sanitize(userInput);
element.innerHTML = clean;
```

---

### ❌ Lỗi 3: Modify NodeList trong vòng lặp

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Live NodeList Mutation</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;"><code>getElementsByClassName()</code> trả về <strong>live NodeList</strong> - tự động update khi DOM thay đổi. Loop và modify cùng lúc → infinite loop hoặc skip elements!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - Live NodeList mutation
const items = document.getElementsByClassName('item');

// Muốn xóa tất cả .item elements
for (let i = 0; i < items.length; i++) {
    items[i].remove();
    // items.length giảm mỗi lần remove
    // → skip elements! Chỉ xóa được 1 nửa
}

console.log(items.length); // Vẫn còn elements! 🤯
```

**Tại sao sai?**
- `items` là **live** NodeList
- `items[0].remove()` → NodeList tự động update
- `i = 1`, nhưng element cũ ở index 1 giờ là index 0
- Loop skip elements!

**Cách fix:**
```javascript
// ✅ ĐÚNG - Cách 1: Convert to Array
const items = Array.from(document.getElementsByClassName('item'));
items.forEach(item => item.remove()); // OK!

// ✅ ĐÚNG - Cách 2: querySelectorAll (static NodeList)
const items = document.querySelectorAll('.item');
items.forEach(item => item.remove()); // OK!

// ✅ ĐÚNG - Cách 3: Loop ngược
const items = document.getElementsByClassName('item');
for (let i = items.length - 1; i >= 0; i--) {
    items[i].remove(); // OK!
}

// ✅ ĐÚNG - Cách 4: Luôn xóa phần tử đầu
const items = document.getElementsByClassName('item');
while (items.length > 0) {
    items[0].remove(); // OK!
}
```

---

### ❌ Lỗi 4: Event listener memory leaks

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Memory Leak</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Thêm event listeners mà không remove khi element bị xóa → memory leak!</p>
</div>

**Ví dụ SAI:**
```javascript
// ❌ SAI - Memory leak
function createButton() {
    const button = document.createElement('button');
    button.textContent = 'Click me';
    
    button.addEventListener('click', () => {
        console.log('Clicked!');
    });
    
    document.body.appendChild(button);
    
    // Remove button sau 5s
    setTimeout(() => {
        button.remove(); // ❌ Listener vẫn còn trong memory!
    }, 5000);
}

// Gọi 1000 lần → 1000 listeners trong memory! 💀
for (let i = 0; i < 1000; i++) {
    createButton();
}
```

**Cách fix:**
```javascript
// ✅ ĐÚNG - Cách 1: Remove listener trước khi remove element
function createButton() {
    const button = document.createElement('button');
    button.textContent = 'Click me';
    
    const handleClick = () => {
        console.log('Clicked!');
    };
    
    button.addEventListener('click', handleClick);
    document.body.appendChild(button);
    
    setTimeout(() => {
        button.removeEventListener('click', handleClick); // ✅
        button.remove();
    }, 5000);
}

// ✅ ĐÚNG - Cách 2: Event delegation (1 listener cho nhiều elements)
document.body.addEventListener('click', (e) => {
    if (e.target.matches('.dynamic-button')) {
        console.log('Clicked!');
    }
}); // Chỉ 1 listener duy nhất!

function createButton() {
    const button = document.createElement('button');
    button.className = 'dynamic-button';
    button.textContent = 'Click me';
    document.body.appendChild(button);
    
    setTimeout(() => {
        button.remove(); // ✅ OK - không leak
    }, 5000);
}

// ✅ ĐÚNG - Cách 3: AbortController (modern)
function createButton() {
    const button = document.createElement('button');
    const controller = new AbortController();
    
    button.addEventListener('click', () => {
        console.log('Clicked!');
    }, { signal: controller.signal });
    
    document.body.appendChild(button);
    
    setTimeout(() => {
        controller.abort(); // ✅ Auto remove listener
        button.remove();
    }, 5000);
}
```
---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** DOM là gì? Khác gì với HTML?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>DOM (Document Object Model):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Tree structure representation của HTML document</li>
      <li>Live, dynamic - có thể thay đổi bằng JavaScript</li>
      <li>Browser API để manipulate webpage</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>HTML:</strong></p>
    <ul style="margin: 0;">
      <li>Text markup language</li>
      <li>Static - file trên server</li>
      <li>Browser parse HTML → tạo DOM</li>
    </ul>
  </div>
</details>

**Câu 2:** querySelector() vs getElementById() - Khác nhau gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Tiêu chí</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">getElementById()</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">querySelector()</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Selector</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Chỉ ID</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Any CSS selector</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Performance</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Nhanh hơn</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Chậm hơn</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Return</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Element hoặc null</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Element hoặc null</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Ví dụ</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><code>getElementById('btn')</code></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><code>querySelector('.btn')</code></td>
      </tr>
    </table>
  </div>
</details>

**Câu 3:** innerHTML vs textContent vs innerText?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>innerHTML:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Get/set HTML markup</li>
      <li>Parse HTML tags</li>
      <li>⚠️ XSS risk với user input</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>textContent:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Get/set text (không parse HTML)</li>
      <li>✅ Safe - auto escape HTML</li>
      <li>✅ Faster than innerHTML</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>innerText:</strong></p>
    <ul style="margin: 0;">
      <li>Like textContent nhưng respect CSS styling</li>
      <li>❌ Slower (trigger reflow)</li>
      <li>Ít dùng, prefer textContent</li>
    </ul>
  </div>
</details>

**Câu 4:** Event bubbling vs Event capturing?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🎈 Event Bubbling (mặc định):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Event từ element → lên parent → ... → document</li>
      <li>Bottom-up propagation</li>
      <li><code>addEventListener('click', handler)</code></li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>📥 Event Capturing:</strong></p>
    <ul style="margin: 0;">
      <li>Event từ document → xuống parent → ... → element</li>
      <li>Top-down propagation</li>
      <li><code>addEventListener('click', handler, true)</code></li>
    </ul>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #e3f2fd; border-radius: 4px;">💡 Dùng <code>event.stopPropagation()</code> để stop propagation</p>
  </div>
</details>

**Câu 5:** Khi nào dùng Event Delegation?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Event Delegation:</strong> Attach 1 listener lên parent thay vì nhiều listeners trên children</p>
    <p style="margin: 0 0 10px 0;"><strong>✅ Dùng khi:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Nhiều child elements cần cùng handler</li>
      <li>Elements được tạo dynamically</li>
      <li>Muốn tránh memory leaks</li>
      <li>Improve performance</li>
    </ul>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 0;"><code>// Thay vì:
document.querySelectorAll('.btn').forEach(btn => {
    btn.addEventListener('click', handler);
});

// Dùng delegation:
document.body.addEventListener('click', (e) => {
    if (e.target.matches('.btn')) {
        handler(e);
    }
});</code></pre>
  </div>
</details>

</div>

---

## Kết luận

DOM Manipulation là kỹ năng cốt lõi trong JavaScript web development:

✅ **Chọn elements** - querySelector/querySelectorAll là tốt nhất  
✅ **Thay đổi content** - innerHTML cho HTML, textContent cho text  
✅ **Thay đổi styles** - classList cho classes, style cho CSS  
✅ **Event handling** - addEventListener cho tất cả events  
✅ **Performance** - Cache references, use event delegation  

**Best Practices:**
- Cache DOM references
- Use event delegation
- Minimize DOM manipulation
- Use classList instead of className
- Check for null before accessing properties

Hãy thực hành nhiều với DOM manipulation - đây là nền tảng để build interactive websites!

---

## Bài tập thực hành

### Bài 1: Change Theme

```html
<button id="themeBtn">Toggle Theme</button>

<!-- Viết code để toggle dark/light theme khi click button -->
```

### Bài 2: Form Validation

```html
<form id="myForm">
  <input type="email" id="email" placeholder="Email">
  <span id="error"></span>
  <button type="submit">Submit</button>
</form>

<!-- Validate email khi submit form -->
```

### Bài 3: Dynamic List

```html
<button id="addBtn">Add Item</button>
<ul id="list"></ul>

<!-- Thêm item mới với số thứ tự tăng dần -->
```

**Đáp án:**

```javascript
// Bài 1
const themeBtn = document.getElementById('themeBtn');
themeBtn.addEventListener('click', () => {
  document.body.classList.toggle('dark-theme');
});

// Bài 2
const form = document.getElementById('myForm');
const email = document.getElementById('email');
const error = document.getElementById('error');

form.addEventListener('submit', (e) => {
  e.preventDefault();
  if (!email.value.includes('@')) {
    error.textContent = 'Invalid email!';
    error.style.color = 'red';
  } else {
    error.textContent = 'Valid!';
    error.style.color = 'green';
  }
});

// Bài 3
let count = 0;
const addBtn = document.getElementById('addBtn');
const list = document.getElementById('list');

addBtn.addEventListener('click', () => {
  count++;
  const li = document.createElement('li');
  li.textContent = `Item ${count}`;
  list.appendChild(li);
});
```

---

## Tài liệu tham khảo

- [MDN - Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [MDN - Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)
- [JavaScript.info - DOM](https://javascript.info/document)
- [W3Schools - DOM Tutorial](https://www.w3schools.com/js/js_htmldom.asp)
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">Kiến thức nền tảng trước khi học DOM</p>
  </div>
</a>

<a href="/posts/bai9" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px;">➡️</div>
    <h4 style="margin: 0 0 10px 0; color: #333; font-size: 20px;">Arrow Functions & ES6</h4>
    <p style="margin: 0; color: #666; font-size: 14px; line-height: 1.6;">Modern JavaScript syntax cho DOM manipulation</p>
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
