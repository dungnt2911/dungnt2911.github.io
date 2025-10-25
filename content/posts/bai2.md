---
title: "Lập trình hướng đối tượng OOP trong Java"
date: 2025-10-10T00:00:00Z
draft: false
---

<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#oop-là-gì">OOP là gì?</a></li>
    <li><a href="#tại-sao-cần-oop">Tại sao cần OOP?</a></li>
    <li><a href="#bốn-tính-chất-cơ-bản-của-oop">Bốn tính chất cơ bản của OOP</a>
      <ul>
        <li><a href="#1-tính-đóng-gói-encapsulation">Tính đóng gói</a></li>
        <li><a href="#2-tính-kế-thừa-inheritance">Tính kế thừa</a></li>
        <li><a href="#3-tính-đa-hình-polymorphism">Tính đa hình</a></li>
        <li><a href="#4-tính-trừu-tượng-abstraction">Tính trừu tượng</a></li>
      </ul>
    </li>
    <li><a href="#class-và-object">Class và Object</a></li>
    <li><a href="#constructor">Constructor</a></li>
    <li><a href="#access-modifiers">Access Modifiers</a></li>
    <li><a href="#getter-và-setter">Getter và Setter</a></li>
    <li><a href="#static-và-final">Static và Final</a></li>
    <li><a href="#ví-dụ-hoàn-chỉnh">Ví dụ hoàn chỉnh</a></li>
    <li><a href="#best-practices">Best Practices</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
  </ol>
</div>

## OOP là gì?

**Lập trình hướng đối tượng (Object-Oriented Programming - OOP)** là một phương pháp lập trình dựa trên khái niệm **đối tượng (objects)** và **lớp (classes)**. 

OOP giúp tổ chức code theo cách gần gũi với thế giới thực, nơi mọi thứ đều là đối tượng có thuộc tính và hành vi.

**Ví dụ thực tế:**
- **Đối tượng:** Con chó
- **Thuộc tính:** Tên, màu lông, tuổi
- **Hành vi:** Sủa, chạy, ăn

## Tại sao cần OOP?

### Ưu điểm của OOP:

✅ **Dễ quản lý:** Code được tổ chức thành các class rõ ràng

✅ **Tái sử dụng:** Kế thừa giúp tái sử dụng code

✅ **Dễ bảo trì:** Sửa đổi một class không ảnh hưởng toàn bộ

✅ **Mở rộng:** Dễ dàng thêm tính năng mới

✅ **Bảo mật:** Đóng gói che giấu thông tin nhạy cảm

### So sánh với lập trình thủ tục:
```java
// ❌ Lập trình thủ tục - Khó quản lý
String studentName = "An";
int studentAge = 20;
double studentGPA = 3.5;

void displayStudent() {
    System.out.println(studentName + " - " + studentAge);
}

// ✅ OOP - Dễ quản lý
class Student {
    private String name;
    private int age;
    private double gpa;
    
    public void display() {
        System.out.println(name + " - " + age);
    }
}
```

## Bốn tính chất cơ bản của OOP

### 1. Tính đóng gói (Encapsulation)

**Định nghĩa:** Che giấu thông tin bên trong đối tượng và chỉ cho phép truy cập thông qua các phương thức public.

**Mục đích:**
- Bảo vệ dữ liệu khỏi truy cập trái phép
- Kiểm soát cách dữ liệu được thay đổi
- Dễ bảo trì và sửa đổi

**Ví dụ:**
```java
class BankAccount {
    // ❌ Không nên public - ai cũng có thể thay đổi
    // public double balance;
    
    // ✅ Nên private - chỉ truy cập qua methods
    private double balance;
    
    // Getter - Đọc dữ liệu
    public double getBalance() {
        return balance;
    }
    
    // Setter - Ghi dữ liệu (có validation)
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            System.out.println("Số tiền không hợp lệ!");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Không đủ tiền!");
        }
    }
}

// Sử dụng
BankAccount account = new BankAccount();
account.deposit(1000);           // ✅ OK
// account.balance = -500;       // ❌ Không thể - balance là private
account.withdraw(200);            // ✅ OK
System.out.println(account.getBalance());  // 800
```
<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Luôn làm fields <code style="background: rgba(255,255,255,0.2); padding: 2px 6px; border-radius: 4px;">private</code> và cung cấp getter/setter public. Điều này cho phép validation, logging và kiểm soát access tốt hơn. Đây là nguyên tắc cốt lõi của Encapsulation!</p>
</div>

**Lợi ích:**
- Dữ liệu được bảo vệ
- Có validation khi thay đổi
- Dễ sửa đổi logic bên trong mà không ảnh hưởng code bên ngoài

---

### 2. Tính kế thừa (Inheritance)

**Định nghĩa:** Cho phép một lớp con (subclass) kế thừa các thuộc tính và phương thức từ lớp cha (superclass).

**Mục đích:**
- Tái sử dụng code
- Tạo mối quan hệ phân cấp
- Mở rộng chức năng

**Ví dụ:**
```java
// Lớp cha (Parent/Super class)
class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ");
    }
}

// Lớp con (Child/Sub class) - kế thừa Animal
class Dog extends Animal {
    private String breed;  // Thuộc tính riêng
    
    public Dog(String name, int age, String breed) {
        super(name, age);  // Gọi constructor của lớp cha
        this.breed = breed;
    }
    
    // Phương thức riêng
    public void bark() {
        System.out.println(name + " đang sủa: Gâu gâu!");
    }
    
    // Override phương thức của lớp cha
    @Override
    public void eat() {
        System.out.println(name + " đang ăn xương");
    }
}

// Lớp con khác
class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age);
    }
    
    public void meow() {
        System.out.println(name + " đang kêu: Meo meo!");
    }
    
    @Override
    public void eat() {
        System.out.println(name + " đang ăn cá");
    }
}

// Sử dụng
Dog dog = new Dog("Lulu", 3, "Husky");
dog.eat();      // Lulu đang ăn xương
dog.sleep();    // Lulu đang ngủ (kế thừa từ Animal)
dog.bark();     // Lulu đang sủa: Gâu gâu!

Cat cat = new Cat("Mimi", 2);
cat.eat();      // Mimi đang ăn cá
cat.meow();     // Mimi đang kêu: Meo meo!
```
<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>Favor composition over inheritance!</strong> Kế thừa tạo tight coupling giữa parent và child class. Chỉ dùng inheritance khi có <strong>is-a relationship</strong> rõ ràng (Dog IS-A Animal). Nếu chỉ cần tái sử dụng code, hãy dùng composition (has-a relationship).</p>
</div>

**Các loại kế thừa trong Java:**
- ✅ Single Inheritance: Dog extends Animal
- ✅ Multilevel Inheritance: Puppy extends Dog extends Animal
- ❌ Multiple Inheritance: KHÔNG hỗ trợ (dùng Interface thay thế)

---

### 3. Tính đa hình (Polymorphism)

**Định nghĩa:** Cho phép các đối tượng khác nhau có thể phản ứng khác nhau với cùng một phương thức.

**Hai loại đa hình:**

#### A. Compile-time Polymorphism (Overloading)

Nhiều phương thức cùng tên nhưng khác tham số.
```java
class Calculator {
    // Cộng 2 số nguyên
    public int add(int a, int b) {
        return a + b;
    }
    
    // Cộng 3 số nguyên
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Cộng 2 số thực
    public double add(double a, double b) {
        return a + b;
    }
}

Calculator calc = new Calculator();
System.out.println(calc.add(5, 3));           // 8
System.out.println(calc.add(5, 3, 2));        // 10
System.out.println(calc.add(5.5, 3.2));       // 8.7
```

#### B. Runtime Polymorphism (Overriding)

Lớp con ghi đè phương thức của lớp cha.
```java
class Shape {
    public void draw() {
        System.out.println("Vẽ hình");
    }
    
    public double area() {
        return 0;
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ hình tròn");
    }
    
    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width, height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Vẽ hình chữ nhật");
    }
    
    @Override
    public double area() {
        return width * height;
    }
}

// Đa hình - Cùng kiểu Shape nhưng hành vi khác nhau
Shape shape1 = new Circle(5);
Shape shape2 = new Rectangle(4, 6);

shape1.draw();  // Vẽ hình tròn
shape2.draw();  // Vẽ hình chữ nhật

System.out.println(shape1.area());  // 78.54
System.out.println(shape2.area());  // 24.0
```
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Polymorphism cho phép viết code flexible và extensible. Khi design system, luôn <strong>code to interface</strong>, không phải implementation. Ví dụ: <code>List<String> list = new ArrayList<>();</code> thay vì <code>ArrayList<String> list = ...</code>. Điều này giúp dễ dàng thay đổi implementation sau này!</p>
</div>

---

### 4. Tính trừu tượng (Abstraction)

**Định nghĩa:** Che giấu các chi tiết phức tạp và chỉ hiển thị các chức năng cần thiết.

**Cách triển khai:**
- Abstract Class
- Interface

#### A. Abstract Class
```java
abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    // Abstract method - không có implementation
    public abstract void start();
    public abstract void stop();
    
    // Concrete method - có implementation
    public void displayInfo() {
        System.out.println("Thương hiệu: " + brand);
    }
}

class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " Car: Khởi động bằng chìa khóa");
    }
    
    @Override
    public void stop() {
        System.out.println(brand + " Car: Dừng bằng phanh");
    }
}

class Motorcycle extends Vehicle {
    public Motorcycle(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " Moto: Khởi động bằng nút bấm");
    }
    
    @Override
    public void stop() {
        System.out.println(brand + " Moto: Dừng bằng phanh tay");
    }
}

// Sử dụng
Vehicle car = new Car("Toyota");
car.start();        // Toyota Car: Khởi động bằng chìa khóa
car.displayInfo();  // Thương hiệu: Toyota

Vehicle moto = new Motorcycle("Honda");
moto.start();       // Honda Moto: Khởi động bằng nút bấm
```

#### B. Interface
```java
interface Flyable {
    void fly();  // public abstract by default
}

interface Swimmable {
    void swim();
}

class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Vịt bay thấp");
    }
    
    @Override
    public void swim() {
        System.out.println("Vịt bơi trên mặt nước");
    }
}

class Fish implements Swimmable {
    @Override
    public void swim() {
        System.out.println("Cá bơi dưới nước");
    }
}

// Sử dụng
Duck duck = new Duck();
duck.fly();   // Vịt bay thấp
duck.swim();  // Vịt bơi trên mặt nước

Fish fish = new Fish();
fish.swim();  // Cá bơi dưới nước
```

---

## Class và Object

### Class là gì?

**Class** là bản thiết kế (blueprint) để tạo ra các đối tượng.
```java
class Student {
    // Thuộc tính (Attributes/Fields)
    private String id;
    private String name;
    private double gpa;
    
    // Constructor
    public Student(String id, String name, double gpa) {
        this.id = id;
        this.name = name;
        this.gpa = gpa;
    }
    
    // Phương thức (Methods)
    public void study() {
        System.out.println(name + " đang học");
    }
    
    public void displayInfo() {
        System.out.println("ID: " + id);
        System.out.println("Tên: " + name);
        System.out.println("GPA: " + gpa);
    }
}
```

### Object là gì?

**Object** là thể hiện cụ thể (instance) của class.
```java
// Tạo objects từ class Student
Student student1 = new Student("SV001", "Nguyễn Văn An", 3.5);
Student student2 = new Student("SV002", "Trần Thị Bình", 3.8);

student1.study();        // Nguyễn Văn An đang học
student1.displayInfo();  // Hiển thị thông tin SV001

student2.study();        // Trần Thị Bình đang học
```

---

## Constructor

**Constructor** là phương thức đặc biệt dùng để khởi tạo object.
```java
class Person {
    private String name;
    private int age;
    
    // Default constructor
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    // Parameterized constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // Constructor overloading
    public Person(String name) {
        this.name = name;
        this.age = 18;  // Tuổi mặc định
    }
}

// Sử dụng
Person p1 = new Person();                    // Default
Person p2 = new Person("An", 25);            // Đầy đủ tham số
Person p3 = new Person("Bình");              // Chỉ tên
```

---

## Access Modifiers

```java
class Example {
    public int publicVar;        // Truy cập ở mọi nơi
    protected int protectedVar;  // Package + subclass
    int defaultVar;              // Chỉ trong package
    private int privateVar;      // Chỉ trong class
}
```

---

## Getter và Setter
```java
class Product {
    private String name;
    private double price;
    
    // Getter
    public String getName() {
        return name;
    }
    
    // Setter với validation
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        }
    }
    
    public double getPrice() {
        return price;
    }
    
    public void setPrice(double price) {
        if (price > 0) {
            this.price = price;
        }
    }
}
```

---

## Static và Final

### Static
```java
class Counter {
    private static int count = 0;  // Biến static - dùng chung
    
    public Counter() {
        count++;
    }
    
    public static int getCount() {  // Method static
        return count;
    }
}

Counter c1 = new Counter();
Counter c2 = new Counter();
System.out.println(Counter.getCount());  // 2
```

### Final
```java
class Constants {
    public static final double PI = 3.14159;  // Hằng số
    public static final String APP_NAME = "MyApp";
}

// Không thể thay đổi
// Constants.PI = 3.14;  // ❌ Lỗi!
```

---

## Ví dụ hoàn chỉnh

### Hệ thống quản lý thư viện
```java
// Lớp cha
abstract class LibraryItem {
    protected String id;
    protected String title;
    protected boolean isAvailable;
    
    public LibraryItem(String id, String title) {
        this.id = id;
        this.title = title;
        this.isAvailable = true;
    }
    
    public abstract void displayInfo();
    
    public void borrow() {
        if (isAvailable) {
            isAvailable = false;
            System.out.println(title + " đã được mượn");
        } else {
            System.out.println(title + " không có sẵn");
        }
    }
    
    public void returnItem() {
        isAvailable = true;
        System.out.println(title + " đã được trả");
    }
}

// Lớp con - Sách
class Book extends LibraryItem {
    private String author;
    private int pages;
    
    public Book(String id, String title, String author, int pages) {
        super(id, title);
        this.author = author;
        this.pages = pages;
    }
    
    @Override
    public void displayInfo() {
        System.out.println("=== SÁCH ===");
        System.out.println("ID: " + id);
        System.out.println("Tên: " + title);
        System.out.println("Tác giả: " + author);
        System.out.println("Số trang: " + pages);
        System.out.println("Trạng thái: " + (isAvailable ? "Có sẵn" : "Đã mượn"));
    }
}

// Lớp con - DVD
class DVD extends LibraryItem {
    private String director;
    private int duration;
    
    public DVD(String id, String title, String director, int duration) {
        super(id, title);
        this.director = director;
        this.duration = duration;
    }
    
    @Override
    public void displayInfo() {
        System.out.println("=== DVD ===");
        System.out.println("ID: " + id);
        System.out.println("Tên: " + title);
        System.out.println("Đạo diễn: " + director);
        System.out.println("Thời lượng: " + duration + " phút");
        System.out.println("Trạng thái: " + (isAvailable ? "Có sẵn" : "Đã mượn"));
    }
}

// Sử dụng
public class LibraryDemo {
    public static void main(String[] args) {
        LibraryItem[] items = new LibraryItem[3];
        
        items[0] = new Book("B001", "Effective Java", "Joshua Bloch", 416);
        items[1] = new Book("B002", "Clean Code", "Robert Martin", 464);
        items[2] = new DVD("D001", "Inception", "Christopher Nolan", 148);
        
        // Hiển thị tất cả
        for (LibraryItem item : items) {
            item.displayInfo();
            System.out.println();
        }
        
        // Mượn sách
        items[0].borrow();  // Effective Java đã được mượn
        items[0].borrow();  // Effective Java không có sẵn
        
        // Trả sách
        items[0].returnItem();  // Effective Java đã được trả
    }
}
```

---

## Best Practices

### 1. Đặt tên Class và Method
```java
// ✅ ĐÚNG - PascalCase cho class
class StudentManager { }

// ✅ ĐÚNG - camelCase cho method
public void calculateGPA() { }

// ❌ SAI
class student_manager { }
public void CalculateGPA() { }
```

### 2. Encapsulation
```java
// ✅ ĐÚNG - Private fields + Public getters/setters
class User {
    private String username;
    
    public String getUsername() {
        return username;
    }
}

// ❌ SAI - Public fields
class User {
    public String username;
}
```

### 3. Constructor
```java
// ✅ ĐÚNG - Validation trong constructor
public Student(String name, double gpa) {
    if (gpa < 0 || gpa > 4.0) {
        throw new IllegalArgumentException("GPA không hợp lệ");
    }
    this.name = name;
    this.gpa = gpa;
}
```

### 4. toString() Method
```java
class Student {
    private String name;
    private double gpa;
    
    @Override
    public String toString() {
        return "Student{name='" + name + "', gpa=" + gpa + "}";
    }
}
```
---

## 🐛 Lỗi thường gặp

### ❌ Lỗi 1: Quên gọi super() trong constructor

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Constructor Chaining</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Quên gọi <code>super()</code> trong constructor của child class. Java tự động gọi <code>super()</code> no-arg, nếu parent không có no-arg constructor → Compile error!</p>
</div>

**Ví dụ lỗi:**
```java
class Animal {
    String name;
    
    // Chỉ có constructor với params
    public Animal(String name) {
        this.name = name;
    }
}

class Dog extends Animal {
    String breed;
    
    // ❌ ERROR! Phải gọi super(name)
    public Dog(String name, String breed) {
        this.breed = breed;  // ❌ Compile error!
    }
}
```

**Cách fix:**
```java
class Dog extends Animal {
    String breed;
    
    // ✅ ĐÚNG - Gọi super() rõ ràng
    public Dog(String name, String breed) {
        super(name);  // ✅ OK
        this.breed = breed;
    }
}
```

---

### ❌ Lỗi 2: Override method với signature khác

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Overriding vs Overloading</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Override method phải có <strong>cùng tên + cùng parameters</strong>. Nếu khác parameters → Overloading (không phải override!)</p>
</div>

**Ví dụ:**
```java
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    // ❌ KHÔNG PHẢI override! (khác parameters)
    // Đây là overload, không phải override
    void makeSound(String tone) {
        System.out.println("Woof in " + tone);
    }
}

// Test
Animal dog = new Dog();
dog.makeSound();  // Output: "Some sound" (không phải "Woof"!)
```

**Cách fix:**
```java
class Dog extends Animal {
    // ✅ ĐÚNG - Override (cùng signature)
    @Override  // Annotation giúp compiler check
    void makeSound() {
        System.out.println("Woof!");
    }
}
```

**💡 Best Practice:** Luôn dùng `@Override` annotation để compiler check!

---

### ❌ Lỗi 3: Không override equals() và hashCode()

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">equals() & hashCode() Contract</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Khi tạo custom objects dùng trong HashMap/HashSet, bắt buộc phải override CẢ HAI <code>equals()</code> và <code>hashCode()</code>!</p>
</div>

---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** 4 nguyên lý OOP là gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <ol style="margin: 0;">
      <li><strong>Encapsulation (Đóng gói):</strong> Ẩn data, cung cấp public methods</li>
      <li><strong>Inheritance (Kế thừa):</strong> Child class kế thừa từ parent</li>
      <li><strong>Polymorphism (Đa hình):</strong> Nhiều hình thái, overriding/overloading</li>
      <li><strong>Abstraction (Trừu tượng):</strong> Ẩn implementation details</li>
    </ol>
  </div>
</details>

**Câu 2:** Overloading vs Overriding - Khác nhau gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse; margin-top: 10px;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Tiêu chí</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Overloading</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Overriding</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Định nghĩa</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Cùng tên, khác parameters</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Cùng tên, cùng parameters</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Vị trí</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Trong cùng 1 class</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Parent & child class</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Thời điểm</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Compile-time</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Runtime</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Return type</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Có thể khác</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Phải giống (hoặc covariant)</td>
      </tr>
    </table>
  </div>
</details>

**Câu 3:** Abstract class vs Interface - Khi nào dùng cái nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🏛️ Abstract Class:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Có thể có concrete methods (implemented)</li>
      <li>Có thể có instance variables</li>
      <li>Single inheritance</li>
      <li>📌 Dùng khi: có shared code, is-a relationship</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🔌 Interface:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Chỉ abstract methods (trước Java 8)</li>
      <li>Chỉ có constants (final variables)</li>
      <li>Multiple implementation</li>
      <li>📌 Dùng khi: define contract, can-do relationship</li>
    </ul>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #e3f2fd; border-radius: 4px;"><strong>💡 Rule of thumb:</strong> Prefer interface unless you need shared implementation!</p>
  </div>
</details>

**Câu 4:** Khi nào nên dùng Inheritance vs Composition?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🔗 Inheritance (is-a):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Dog IS-A Animal</li>
      <li>✅ Car IS-A Vehicle</li>
      <li>❌ Tạo tight coupling</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🧩 Composition (has-a):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Car HAS-A Engine</li>
      <li>✅ Person HAS-A Address</li>
      <li>✅ Loose coupling, flexible</li>
    </ul>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #d4edda; border-radius: 4px;"><strong>✅ Best Practice:</strong> "Favor composition over inheritance" - Effective Java</p>
  </div>
</details>

**Câu 5:** Access modifiers - private, protected, public, default?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Modifier</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Class</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Package</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">Subclass</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">World</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>public</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>protected</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>default</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><strong>private</strong></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌</td>
      </tr>
    </table>
  </div>
</details>

</div>

## Kết luận

OOP là nền tảng quan trọng trong Java và các ngôn ngữ lập trình hiện đại. Hiểu rõ 4 tính chất cơ bản sẽ giúp bạn:

✅ Viết code dễ quản lý và bảo trì

✅ Tái sử dụng code hiệu quả

✅ Xây dựng ứng dụng mở rộng được

✅ Làm việc tốt hơn với các framework


### Tài liệu tham khảo

- Oracle Java Documentation - OOP Concepts
- Effective Java by Joshua Bloch
- Head First Java
- Clean Code by Robert C. Martin