---
title: "Giới thiệu Java - Từ cơ bản đến nâng cao"
date: 2025-10-10T00:00:00Z
draft: false
---

<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#java-là-gì">Java là gì?</a></li>
    <li><a href="#lịch-sử-phát-triển">Lịch sử phát triển</a></li>
    <li><a href="#tại-sao-nên-học-java">Tại sao nên học Java?</a></li>
    <li><a href="#đặc-điểm-nổi-bật-của-java">Đặc điểm nổi bật của Java</a></li>
    <li><a href="#jdk-jre-và-jvm">JDK, JRE và JVM</a></li>
    <li><a href="#cài-đặt-môi-trường-java">Cài đặt môi trường Java</a></li>
    <li><a href="#chương-trình-java-đầu-tiên">Chương trình Java đầu tiên</a></li>
    <li><a href="#cú-pháp-cơ-bản">Cú pháp cơ bản</a></li>
    <li><a href="#kiểu-dữ-liệu">Kiểu dữ liệu</a></li>
    <li><a href="#toán-tử">Toán tử</a></li>
    <li><a href="#cấu-trúc-điều-khiển">Cấu trúc điều khiển</a></li>
    <li><a href="#ứng-dụng-của-java">Ứng dụng của Java</a></li>
    <li><a href="#so-sánh-java-với-các-ngôn-ngữ-khác">So sánh Java với các ngôn ngữ khác</a></li>
    <li><a href="#roadmap-học-java">Roadmap học Java</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
  </ol>
</div>

## Java là gì?

**Java** là một ngôn ngữ lập trình hướng đối tượng (Object-Oriented Programming) được phát triển bởi **Sun Microsystems** (nay thuộc Oracle) vào năm 1995.

### Khẩu hiệu của Java:

> **"Write Once, Run Anywhere" (WORA)**
> 
> Viết một lần, chạy mọi nơi!

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Java là ngôn ngữ <strong>"Write Once, Run Anywhere"</strong> - code Java có thể chạy trên bất kỳ nền tảng nào có JVM (Windows, Mac, Linux). Đây là lý do tại sao Java được dùng rộng rãi trong enterprise applications và Android development!</p>
</div>

### Ví dụ minh họa:
```java
// Code này chạy được trên:
// ✅ Windows
// ✅ macOS  
// ✅ Linux
// ✅ Android
// ✅ Raspberry Pi

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

---

## Lịch sử phát triển

### Timeline quan trọng:

📅 **1991:** Dự án bắt đầu bởi James Gosling tại Sun Microsystems với tên "Oak"

📅 **1995:** Java 1.0 ra mắt chính thức

📅 **1996:** Java 1.1 - Thêm JDBC, RMI

📅 **1998:** Java 2 (J2SE 1.2) - Swing, Collections Framework

📅 **2004:** Java 5 - Generics, Annotations, Enum

📅 **2010:** Oracle mua lại Sun Microsystems

📅 **2014:** Java 8 - Lambda expressions, Stream API, Optional

📅 **2017:** Java 9 - Module system

📅 **2018:** Java 10, 11 (LTS)

📅 **2021:** Java 17 (LTS - Long Term Support)

📅 **2023:** Java 21 (LTS) - Virtual Threads, Pattern Matching

📅 **2024:** Java 22

### Các phiên bản LTS quan trọng:

- **Java 8** (2014) - Phổ biến nhất
- **Java 11** (2018) - LTS
- **Java 17** (2021) - LTS hiện tại khuyên dùng
- **Java 21** (2023) - LTS mới nhất

---

## Tại sao nên học Java?

### 1. 🌍 Phổ biến toàn cầu

- **#3** ngôn ngữ phổ biến nhất thế giới (theo TIOBE Index)
- **9+ triệu** lập trình viên Java trên toàn cầu
- **Top 3** ngôn ngữ được yêu cầu nhất trong tuyển dụng

### 2. 💼 Nhu cầu việc làm cao
```
📊 Thống kê việc làm Java (2024):

✅ Backend Developer
✅ Android Developer  
✅ Enterprise Application Developer
✅ Cloud Engineer
✅ Big Data Engineer
✅ DevOps Engineer

💰 Mức lương trung bình:
- Junior: $50k - $70k/năm
- Mid: $70k - $100k/năm
- Senior: $100k - $150k+/năm
```

### 3. 🏢 Được sử dụng bởi các công ty lớn

- **Google** - Android OS, nhiều dịch vụ backend
- **Netflix** - Streaming platform
- **Amazon** - E-commerce, AWS services
- **LinkedIn** - Social network
- **Uber** - Backend services
- **Airbnb** - Backend infrastructure
- **Twitter** - Một phần backend
- **eBay** - E-commerce platform

### 4. 📚 Tài liệu phong phú

- Documentation chính thức từ Oracle
- Hàng triệu bài viết, tutorial
- Cộng đồng Stack Overflow lớn
- Nhiều sách hay (Effective Java, Head First Java)

### 5. 🔧 Hệ sinh thái mạnh mẽ

- **Spring Framework** - Enterprise applications
- **Hibernate** - ORM
- **Maven/Gradle** - Build tools
- **JUnit** - Testing
- **Apache Kafka** - Streaming
- **Apache Spark** - Big Data

---

## Đặc điểm nổi bật của Java

### 1. ⚡ Đơn giản (Simple)

Java loại bỏ các tính năng phức tạp như pointer, operator overloading.
```java
// Java - Đơn giản, rõ ràng
String name = "John";
System.out.println(name);

// So với C++ - Phức tạp hơn với pointer
// char* name = "John";
// cout << name;
```

### 2. 🎯 Hướng đối tượng (Object-Oriented)

Mọi thứ trong Java đều là object (trừ primitive types).
```java
class Dog {
    String name;
    int age;
    
    void bark() {
        System.out.println(name + " says: Woof!");
    }
}

Dog myDog = new Dog();
myDog.name = "Buddy";
myDog.bark();  // Buddy says: Woof!
```

### 3. 🛡️ An toàn (Secure)

- Không có pointer → Không thể truy cập bộ nhớ trực tiếp
- Security Manager kiểm soát quyền truy cập
- Bytecode verification trước khi chạy

### 4. 🌐 Độc lập nền tảng (Platform Independent)
```
┌─────────────┐
│ Java Code   │
│  (.java)    │
└──────┬──────┘
       │ javac (compile)
       ▼
┌─────────────┐
│  Bytecode   │
│  (.class)   │
└──────┬──────┘
       │
   ┌───┴────┬─────────┬──────────┐
   ▼        ▼         ▼          ▼
  JVM      JVM       JVM        JVM
Windows  macOS    Linux    Android
```

### 5. 🚀 Hiệu năng cao (High Performance)

- **JIT Compiler** - Biên dịch bytecode sang native code khi chạy
- **Garbage Collection** - Tự động quản lý bộ nhớ
- **Multithreading** - Hỗ trợ đa luồng

### 6. 📦 Phân tán (Distributed)

Dễ dàng tạo ứng dụng phân tán với RMI, EJB, Web Services.
```java
// Gọi method từ máy chủ từ xa
RemoteService service = (RemoteService) 
    Naming.lookup("rmi://server.com/MyService");
service.doSomething();
```

### 7. 🔄 Đa luồng (Multithreaded)
```java
// Tạo thread dễ dàng
Thread thread = new Thread(() -> {
    System.out.println("Running in thread: " + 
        Thread.currentThread().getName());
});
thread.start();
```

### 8. 🎭 Động (Dynamic)

Java hỗ trợ tải class động (dynamic class loading) khi runtime.

---

## JDK, JRE và JVM

### 1. **JVM** - Java Virtual Machine

- Thực thi Java bytecode
- Quản lý bộ nhớ
- Garbage Collection
- Platform-specific (mỗi OS có JVM riêng)

### 2. **JRE** - Java Runtime Environment

- JVM + Libraries + Files
- Để **chạy** Java applications
- Không có compiler

### 3. **JDK** - Java Development Kit

- JRE + Development Tools
- Để **phát triển** Java applications
- Có compiler (javac)

**Kết luận:**
- Nếu chỉ chạy Java → Cài **JRE**
- Nếu phát triển Java → Cài **JDK**

---

<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>Đừng nhầm lẫn JDK vs JRE!</strong> Để <strong>chạy</strong> Java app → cần JRE. Để <strong>phát triển</strong> Java app → cần JDK (JDK bao gồm JRE + compiler + tools). Luôn cài JDK khi làm developer!</p>
</div>

## Cài đặt môi trường Java

### Bước 1: Download JDK

🔗 **Link download:**
- Oracle JDK: https://www.oracle.com/java/technologies/downloads/
- OpenJDK: https://adoptium.net/

**Khuyến nghị:** Java 17 LTS hoặc Java 21 LTS

### Bước 2: Cài đặt

#### Windows:
1. Download file `.exe`
2. Chạy installer
3. Chọn đường dẫn cài đặt (mặc định: `C:\Program Files\Java\jdk-17`)
4. Next → Install

#### macOS:
```bash
# Dùng Homebrew
brew install openjdk@17

# Hoặc download từ website và cài .dmg
```

#### Linux (Ubuntu):
```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

### Bước 3: Thiết lập biến môi trường

#### Windows:
1. Chuột phải **This PC** → **Properties**
2. **Advanced system settings** → **Environment Variables**
3. Thêm biến:
   - `JAVA_HOME` = `C:\Program Files\Java\jdk-17`
   - Thêm vào `Path`: `%JAVA_HOME%\bin`

#### macOS/Linux:
```bash
# Thêm vào ~/.bashrc hoặc ~/.zshrc
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```

### Bước 4: Kiểm tra
```bash
java -version
# Output: java version "17.0.x"

javac -version
# Output: javac 17.0.x
```

---

## Chương trình Java đầu tiên

### 1. Tạo file HelloWorld.java
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.out.println("Welcome to Java!");
    }
}
```
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Luôn đặt tên class <strong>giống với tên file</strong> (case-sensitive!). File <code>HelloWorld.java</code> phải chứa <code>public class HelloWorld</code>. Đây là rule bắt buộc trong Java để compiler có thể tìm thấy class!</p>
</div>

### 2. Biên dịch
```bash
javac HelloWorld.java
# Tạo ra file HelloWorld.class (bytecode)
```

### 3. Chạy
```bash
java HelloWorld
# Output:
# Hello, World!
# Welcome to Java!
```

### Giải thích từng dòng:
```java
public class HelloWorld {          // 1. Khai báo class
    public static void main(        // 2. Main method - điểm bắt đầu
        String[] args               // 3. Tham số dòng lệnh
    ) {
        System.out.println(         // 4. In ra console
            "Hello, World!"
        );
    }
}
```

**Lưu ý:**
- Tên file **phải trùng** với tên class public: `HelloWorld.java`
- Java **phân biệt chữ hoa/thường**: `HelloWorld` ≠ `helloworld`

---

## Cú pháp cơ bản

### 1. Comments (Chú thích)
```java
// Single-line comment

/*
   Multi-line comment
   Line 2
*/

/**
 * Javadoc comment
 * @author Your Name
 * @version 1.0
 */
```

### 2. Khai báo biến
```java
// Syntax: dataType variableName = value;

int age = 25;
double salary = 50000.5;
String name = "John";
boolean isStudent = true;
char grade = 'A';
```

### 3. Naming Conventions
```java
// ✅ ĐÚNG
class StudentManager { }          // PascalCase cho class
int studentAge = 20;              // camelCase cho biến
final double PI = 3.14159;        // UPPER_CASE cho hằng số
void calculateTotal() { }         // camelCase cho method

// ❌ SAI
class student_manager { }
int StudentAge = 20;
void CalculateTotal() { }
```

### 4. Semicolon (;)
```java
// Java YÊU CẦU dấu ; ở cuối mỗi statement
int x = 5;              // ✅
System.out.println(x);  // ✅

int y = 10              // ❌ Thiếu ;
```

---

## Kiểu dữ liệu

### 1. Primitive Types (Kiểu nguyên thủy)

| Type | Size | Range | Default | Example |
|------|------|-------|---------|---------|
| byte | 8 bit | -128 to 127 | 0 | `byte b = 100;` |
| short | 16 bit | -32,768 to 32,767 | 0 | `short s = 1000;` |
| int | 32 bit | -2³¹ to 2³¹-1 | 0 | `int i = 100000;` |
| long | 64 bit | -2⁶³ to 2⁶³-1 | 0L | `long l = 100000L;` |
| float | 32 bit | ~±3.4e38 | 0.0f | `float f = 3.14f;` |
| double | 64 bit | ~±1.7e308 | 0.0d | `double d = 3.14;` |
| boolean | 1 bit | true/false | false | `boolean b = true;` |
| char | 16 bit | 0 to 65,535 | '\u0000' | `char c = 'A';` |

### 2. Reference Types (Kiểu tham chiếu)
```java
String name = "Java";           // String
int[] numbers = {1, 2, 3};      // Array
ArrayList<String> list = new ArrayList<>();  // Object
```

### 3. Type Casting
```java
// Widening (tự động)
int i = 100;
double d = i;  // 100.0

// Narrowing (phải ép kiểu)
double d = 100.5;
int i = (int) d;  // 100 (mất phần thập phân)
```

---

## Toán tử

### 1. Arithmetic Operators (Toán tử số học)
```java
int a = 10, b = 3;

System.out.println(a + b);  // 13 - Cộng
System.out.println(a - b);  // 7  - Trừ
System.out.println(a * b);  // 30 - Nhân
System.out.println(a / b);  // 3  - Chia (nguyên)
System.out.println(a % b);  // 1  - Chia lấy dư

a++;  // 11 - Tăng 1
b--;  // 2  - Giảm 1
```

### 2. Comparison Operators (Toán tử so sánh)
```java
int x = 5, y = 10;

System.out.println(x == y);  // false - Bằng
System.out.println(x != y);  // true  - Khác
System.out.println(x > y);   // false - Lớn hơn
System.out.println(x < y);   // true  - Nhỏ hơn
System.out.println(x >= y);  // false - Lớn hơn hoặc bằng
System.out.println(x <= y);  // true  - Nhỏ hơn hoặc bằng
```

### 3. Logical Operators (Toán tử logic)
```java
boolean a = true, b = false;

System.out.println(a && b);  // false - AND
System.out.println(a || b);  // true  - OR
System.out.println(!a);      // false - NOT
```

### 4. Assignment Operators (Toán tử gán)
```java
int x = 10;

x += 5;  // x = x + 5  → 15
x -= 3;  // x = x - 3  → 12
x *= 2;  // x = x * 2  → 24
x /= 4;  // x = x / 4  → 6
x %= 4;  // x = x % 4  → 2
```

---

## Cấu trúc điều khiển

### 1. If-Else
```java
int score = 85;

if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else if (score >= 70) {
    System.out.println("C");
} else {
    System.out.println("F");
}
```

### 2. Switch
```java
String day = "Monday";

switch (day) {
    case "Monday":
        System.out.println("Start of work week");
        break;
    case "Friday":
        System.out.println("TGIF!");
        break;
    case "Saturday":
    case "Sunday":
        System.out.println("Weekend!");
        break;
    default:
        System.out.println("Midweek");
}

// Java 14+ - Switch expression
String result = switch (day) {
    case "Monday" -> "Start of work week";
    case "Friday" -> "TGIF!";
    case "Saturday", "Sunday" -> "Weekend!";
    default -> "Midweek";
};
```

### 3. For Loop
```java
// Traditional for
for (int i = 0; i < 5; i++) {
    System.out.println(i);  // 0 1 2 3 4
}

// Enhanced for (for-each)
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

### 4. While Loop
```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

### 5. Do-While Loop
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

---

## Ứng dụng của Java

### 1. 📱 Mobile Applications

- **Android Apps** - Hầu hết apps Android viết bằng Java
- Kotlin (ngôn ngữ mới cho Android) chạy trên JVM

### 2. 🌐 Web Applications

- **Backend**: Spring Boot, Java EE, JSP, Servlets
- **Enterprise**: Banking, E-commerce, Government
- **Examples**: LinkedIn, Amazon, eBay

### 3. 🖥️ Desktop Applications

- **GUI**: JavaFX, Swing
- **IDEs**: IntelliJ IDEA, Eclipse, NetBeans
- **Tools**: Android Studio

### 4. ☁️ Cloud & Microservices

- **Spring Cloud** - Microservices framework
- **AWS Lambda** - Serverless
- **Google Cloud Functions**

### 5. 📊 Big Data

- **Apache Hadoop** - Distributed storage
- **Apache Spark** - Data processing
- **Apache Kafka** - Streaming platform
- **Elasticsearch** - Search engine

### 6. 🤖 IoT (Internet of Things)

- **Java ME** - Embedded systems
- **Raspberry Pi** projects

### 7. 🎮 Game Development

- **Minecraft** - Viết bằng Java
- **LibGDX** - Game framework

---

## So sánh Java với các ngôn ngữ khác

### Java vs Python

| Feature | Java | Python |
|---------|------|--------|
| Typing | Static (compile-time) | Dynamic (runtime) |
| Performance | Nhanh hơn | Chậm hơn |
| Syntax | Dài dòng | Ngắn gọn |
| Use case | Enterprise, Android | AI/ML, Data Science |
| Learning curve | Trung bình | Dễ hơn |
```java
// Java - Verbose
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}

# Python - Concise
print("Hello")
```

### Java vs JavaScript

| Feature | Java | JavaScript |
|---------|------|------------|
| Type | Compiled | Interpreted |
| Platform | Backend, Mobile | Frontend, Backend (Node.js) |
| Typing | Static | Dynamic |
| Threading | Multi-threaded | Single-threaded (với async) |

### Java vs C++

| Feature | Java | C++ |
|---------|------|-----|
| Memory | Garbage Collection | Manual |
| Pointers | No | Yes |
| Multiple Inheritance | No (Interface only) | Yes |
| Platform | WORA | Platform-dependent |

---

## Roadmap học Java

### 🎯 Beginner (1-2 tháng)
```
✅ Cài đặt JDK
✅ Cú pháp cơ bản
✅ Kiểu dữ liệu, biến
✅ Operators, Control flow
✅ Arrays, Strings
✅ Methods
✅ OOP basics (Class, Object)
```

### 🎯 Intermediate (2-3 tháng)
```
✅ OOP nâng cao (Inheritance, Polymorphism, Abstraction, Encapsulation)
✅ Exception Handling
✅ Collections Framework (List, Set, Map)
✅ Generics
✅ File I/O
✅ Lambda & Stream API
✅ Multithreading
```

### 🎯 Advanced (3-6 tháng)
```
✅ JDBC - Database connectivity
✅ Servlets & JSP
✅ Spring Framework
✅ Spring Boot
✅ RESTful APIs
✅ Microservices
✅ JUnit Testing
✅ Maven/Gradle
✅ Git/GitHub
```

### 🎯 Expert (6+ tháng)
```
✅ Design Patterns
✅ Spring Cloud
✅ Docker & Kubernetes
✅ CI/CD
✅ Kafka, RabbitMQ
✅ Redis, Elasticsearch
✅ System Design
✅ Cloud (AWS, Azure, GCP)
```
---

## 🐛 Lỗi thường gặp cho người mới học Java

### ❌ Lỗi 1: Tên file không khớp với tên class

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">File Name Mismatch</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Lỗi phổ biến nhất với người mới! File name phải <strong>GIỐNG CHÍNH XÁC</strong> với public class name (case-sensitive).</p>
</div>

**Ví dụ lỗi:**
```java
// File: helloworld.java (sai - chữ thường)
public class HelloWorld {  // ❌ Không khớp!
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

**Lỗi compile:**
```
error: class HelloWorld is public, should be declared in a file named HelloWorld.java
```

**Cách fix:**
```java
// File: HelloWorld.java (đúng - chữ hoa H và W)
public class HelloWorld {  // ✅ Khớp!
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

---

### ❌ Lỗi 2: Quên main() method

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Missing main() Method</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Java application phải có <code>main()</code> method với signature chính xác để chạy được!</p>
</div>

**Ví dụ lỗi:**
```java
public class Test {
    // ❌ SAI - Không có main() method
    public void start() {
        System.out.println("Hello");
    }
}
```

**Lỗi runtime:**
```
Error: Main method not found in class Test
```

**Cách fix:**
```java
public class Test {
    // ✅ ĐÚNG - main() method với signature đúng
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

**💡 Nhớ:** `main()` phải là: `public static void main(String[] args)`

---

### ❌ Lỗi 3: Sai cú pháp String[] args

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Main Method Signature</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">main() method phải có ĐÚNG signature: <code>public static void main(String[] args)</code></p>
</div>

**Các cách viết đúng:**
```java
// ✅ Tất cả đều OK
public static void main(String[] args)
public static void main(String args[])
public static void main(String... args)
```

**Các cách viết SAI:**
```java
// ❌ SAI
public void main(String[] args)        // Thiếu static
static void main(String[] args)        // Thiếu public
public static int main(String[] args)  // Sai return type
public static void main()              // Thiếu parameter
```

---
---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** JDK, JRE và JVM khác nhau như thế nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🔧 JDK (Java Development Kit):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Bao gồm JRE + compiler (javac) + development tools</li>
      <li>📌 Dùng khi: Phát triển Java applications</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🏃 JRE (Java Runtime Environment):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Bao gồm JVM + libraries để chạy Java apps</li>
      <li>📌 Dùng khi: Chỉ cần chạy Java applications</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>⚙️ JVM (Java Virtual Machine):</strong></p>
    <ul style="margin: 0;">
      <li>Máy ảo chạy bytecode (.class files)</li>
      <li>📌 Là nền tảng của "Write Once, Run Anywhere"</li>
    </ul>
  </div>
</details>

**Câu 2:** Java là compiled hay interpreted language?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>✅ CẢ HAI!</strong></p>
    <ol style="margin: 0;">
      <li><strong>Compiled:</strong> <code>.java</code> → <code>javac</code> → <code>.class</code> (bytecode)</li>
      <li><strong>Interpreted:</strong> JVM đọc bytecode và thực thi</li>
    </ol>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #e3f2fd; border-radius: 4px;">💡 Java là <strong>compiled language</strong> (compile to bytecode) + JVM là <strong>interpreter</strong> (execute bytecode)</p>
  </div>
</details>

**Câu 3:** Tại sao main() method phải là static?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0;">main() phải là <code>static</code> vì JVM gọi main() <strong>TRƯỚC KHI</strong> tạo bất kỳ object nào. Static methods có thể gọi mà không cần tạo instance của class.</p>
    <p style="margin: 10px 0 0 0;"><strong>Nếu không static:</strong> JVM phải tạo object trước → Nhưng không biết constructor nào để gọi → Chicken-egg problem!</p>
  </div>
</details>

**Câu 4:** "Write Once, Run Anywhere" nghĩa là gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;">Code Java compile thành <strong>bytecode</strong> (platform-independent). Bytecode này có thể chạy trên bất kỳ OS nào có JVM:</p>
    <ul style="margin: 0;">
      <li>✅ Viết code 1 lần trên Windows</li>
      <li>✅ Compile thành .class files</li>
      <li>✅ Chạy trên Windows, Mac, Linux mà không cần sửa code!</li>
    </ul>
  </div>
</details>

**Câu 5:** Sự khác biệt giữa System.out.print() và System.out.println()?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong><code>print()</code>:</strong> In ra KHÔNG xuống dòng</p>
    <p style="margin: 0;"><strong><code>println()</code>:</strong> In ra VÀ xuống dòng (line = ln)</p>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 10px 0 0 0;"><code>System.out.print("Hello ");
System.out.print("World");  // Output: Hello World

System.out.println("Hello");
System.out.println("World"); // Output:
                             // Hello
                             // World</code></pre>
  </div>
</details>

</div>

## Kết luận

Java là một ngôn ngữ mạnh mẽ và phổ biến với nhiều ưu điểm:

**Đa nền tảng** - Write Once, Run Anywhere

**An toàn** - Memory management, Security

**Hiệu năng cao** - JIT compiler, Optimizations

**Hệ sinh thái phong phú** - Frameworks, Libraries

**Cộng đồng lớn** - Support, Resources

**Việc làm nhiều** - High demand in job market

### Lời khuyên cho người mới bắt đầu:

1. **Thực hành mỗi ngày** - Code ít nhất 1 giờ/ngày
2. **Làm projects nhỏ** - Todo app, Calculator, Library Management
3. **Đọc code người khác** - GitHub, Open source
4. **Tham gia cộng đồng** - Stack Overflow, Reddit, Discord
5. **Học từ sai lầm** - Debug là kỹ năng quan trọng
6. **Kiên nhẫn** - Programming là marathon, không phải sprint

### Tài liệu học tập:

📚 **Sách:**
- "Head First Java" - Kiran & Bert Bates
- "Effective Java" - Joshua Bloch
- "Java: The Complete Reference" - Herbert Schildt
- "Clean Code" - Robert C. Martin

🎥 **Khóa học online:**
- Java Programming Masterclass (Udemy)
- Java Tutorial for Complete Beginners (Udemy)
- Java Programming (Coursera)
- freeCodeCamp - Java Tutorial

🌐 **Websites:**
- https://docs.oracle.com/javase/ (Official docs)
- https://www.baeldung.com/ (Tutorials)
- https://www.geeksforgeeks.org/java/
- https://stackoverflow.com/questions/tagged/java
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai2" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">☕</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Java Collections Framework</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">ArrayList, HashMap, LinkedList - Collections trong Java</p>
  </div>
</a>

<a href="/posts/bai3" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🏛️</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">OOP Principles trong Java</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">4 nguyên lý OOP: Encapsulation, Inheritance, Polymorphism, Abstraction</p>
  </div>
</a>

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">Kiến thức nền tảng về JavaScript</p>
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

**Chúc bạn học Java thành công!** 🎉

### Bài tiếp theo:

👉 [Bài 2: Lập trình hướng đối tượng OOP trong Java](/posts/bai2/)