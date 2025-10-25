---
title: "Lambda va Stream API"
date: 2025-10-10T04:00:00Z
draft: false
---
<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#giới-thiệu">Giới thiệu</a></li>
    <li><a href="#lambda-expression---biểu-thức-lambda">Lambda Expression - Biểu thức Lambda</a></li>
    <li><a href="#cú-pháp-cơ-bản">Cú pháp cơ bản</a></li>
    <li><a href="#ví-dụ-so-sánh-trước-và-sau-lambda">Ví dụ so sánh: Trước và sau Lambda</a></li>
    <li><a href="#functional-interface">Functional Interface</a></li>
    <li><a href="#built-in-functional-interfaces">Built-in Functional Interfaces</a></li>
    <li><a href="#stream-api---xử-lý-dữ-liệu-theo-luồng">Stream API - Xử lý dữ liệu theo luồng</a>
      <ul>
        <li><a href="#stream-là-gì">Stream là gì?</a></li>
        <li><a href="#đặc-điểm-của-stream">Đặc điểm của Stream</a></li>
        <li><a href="#tạo-stream">Tạo Stream</a></li>
        <li><a href="#các-thao-tác-trên-stream">Các thao tác trên Stream</a></li>
      </ul>
    </li>
    <li><a href="#ví-dụ-thực-tế-với-class">Ví dụ thực tế với Class</a></li>
    <li><a href="#collectors---thu-thập-kết-quả">Collectors - Thu thập kết quả</a></li>
    <li><a href="#parallel-stream---xử-lý-song-song">Parallel Stream - Xử lý song song</a></li>
    <li><a href="#lỗi-thường-gặp-common-mistakes">Lỗi thường gặp (Common Mistakes)</a></li>
    <li><a href="#best-practices---cách-viết-tốt">Best Practices - Cách viết tốt</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#ví-dụ-nâng-cao">Ví dụ nâng cao</a></li>
    <li><a href="#tips--tricks">Tips & Tricks</a></li>
    <li><a href="#so-sánh-trước-và-sau-stream-api">So sánh: Trước và sau Stream API</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## Giới thiệu
Lambda expression và Stream API là hai tính năng cực kỳ quan trọng được giới thiệu từ Java 8, đánh dấu bước ngoặt lớn trong cách viết code Java hiện đại. Chúng giúp lập trình viên viết code ngắn gọn, dễ đọc hơn và hỗ trợ mạnh mẽ cho lập trình hàm (functional programming).
Trước Java 8, để thực hiện các thao tác đơn giản như sắp xếp danh sách hay lọc dữ liệu, chúng ta phải viết rất nhiều boilerplate code. Lambda và Stream API đã thay đổi hoàn toàn điều này.

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Lambda expressions là <strong>game changer</strong> trong Java 8! Chúng biến code từ verbose thành concise, từ imperative thành functional. Code như <code>(x, y) -> x + y</code> ngắn gọn hơn 10x so với anonymous class. Đây là bước tiến lớn giúp Java hiện đại và competitive với các ngôn ngữ khác!</p>
</div>

### Lambda Expression - Biểu thức Lambda
#### Lambda là gì?
Lambda expression là một hàm ẩn danh (anonymous function) - tức là hàm không có tên. Nó cho phép bạn truyền hành vi như một tham số, giúp code ngắn gọn và linh hoạt hơn.
### Cú pháp cơ bản
````java
// Cú pháp chung
(parameters) -> expression

// Hoặc với nhiều câu lệnh
(parameters) -> {
    statements;
    return value;
}
````
### Ví dụ so sánh: Trước và sau Lambda
#### Cách truyền thống (trước Java 8):
````java
// Sắp xếp danh sách tên
List<String> names = Arrays.asList("Dung", "An", "Binh", "Chau");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

System.out.println(names); // [An, Binh, Chau, Dung]
````
#### Với Lambda (Java 8+):
````java
List<String> names = Arrays.asList("Dung", "An", "Binh", "Chau");

// Ngắn gọn và dễ hiểu hơn rất nhiều!
Collections.sort(names, (a, b) -> a.compareTo(b));

// Hoặc còn ngắn hơn với method reference
Collections.sort(names, String::compareTo);

System.out.println(names); // [An, Binh, Chau, Dung]
````
#### Các dạng Lambda Expression
````java
// 1. Không có tham số
() -> System.out.println("Hello Lambda!");

// 2. Một tham số (có thể bỏ ngoặc đơn)
x -> x * x
(x) -> x * x  // Cả hai đều đúng

// 3. Nhiều tham số
(x, y) -> x + y

// 4. Có kiểu dữ liệu rõ ràng
(int x, int y) -> x + y

// 5. Nhiều câu lệnh (cần dùng dấu ngoặc nhọn và return)
(x, y) -> {
    int sum = x + y;
    return sum * 2;
}
````
#### Functional Interface
Lambda chỉ hoạt động với functional interface - interface có duy nhất một phương thức trừu tượng (abstract method).

<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Sử dụng built-in functional interfaces (<code>Predicate</code>, <code>Function</code>, <code>Consumer</code>, <code>Supplier</code>) thay vì tự tạo! Java cung cấp sẵn 43+ functional interfaces trong <code>java.util.function</code> package. Điều này giúp code consistent, readable và tận dụng được method references!</p>
</div>

````java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class LambdaDemo {
    public static void main(String[] args) {
        // Cách cũ
        Calculator oldAdd = new Calculator() {
            @Override
            public int calculate(int a, int b) {
                return a + b;
            }
        };
        
        // Với Lambda - ngắn gọn hơn nhiều!
        Calculator add = (a, b) -> a + b;
        Calculator subtract = (a, b) -> a - b;
        Calculator multiply = (a, b) -> a * b;
        Calculator divide = (a, b) -> a / b;
        
        System.out.println("5 + 3 = " + add.calculate(5, 3));        // 8
        System.out.println("5 - 3 = " + subtract.calculate(5, 3));   // 2
        System.out.println("5 * 3 = " + multiply.calculate(5, 3));   // 15
        System.out.println("6 / 3 = " + divide.calculate(6, 3));     // 2
    }
}
````
### Built-in Functional Interfaces
Java cung cấp sẵn nhiều functional interface trong package
````java
import java.util.function.*;

public class FunctionalInterfaceDemo {
    public static void main(String[] args) {
        // 1. Predicate<T> - Kiểm tra điều kiện, trả về boolean
        Predicate<Integer> isEven = n -> n % 2 == 0;
        System.out.println(isEven.test(4));  // true
        System.out.println(isEven.test(7));  // false
        
        // 2. Function<T, R> - Nhận đầu vào T, trả về R
        Function<String, Integer> stringLength = s -> s.length();
        System.out.println(stringLength.apply("Hello"));  // 5
        
        // 3. Consumer<T> - Nhận đầu vào, không trả về gì
        Consumer<String> printer = s -> System.out.println("Message: " + s);
        printer.accept("Hello Lambda");  // Message: Hello Lambda
        
        // 4. Supplier<T> - Không nhận đầu vào, trả về T
        Supplier<Double> randomValue = () -> Math.random();
        System.out.println(randomValue.get());  // số ngẫu nhiên
        
        // 5. BiFunction<T, U, R> - Nhận 2 đầu vào T và U, trả về R
        BiFunction<Integer, Integer, Integer> sum = (a, b) -> a + b;
        System.out.println(sum.apply(10, 20));  // 30
    }
}
````
### Stream API - Xử lý dữ liệu theo luồng
#### Stream là gì?
Stream API cho phép xử lý collection (danh sách) theo phong cách functional programming. Nó giống như một "dây chuyền sản xuất" nơi dữ liệu được xử lý qua nhiều bước.
### Đặc điểm của Stream

Không lưu trữ dữ liệu - Stream không phải là cấu trúc dữ liệu

Không thay đổi nguồn - Không làm thay đổi collection gốc

Lazy evaluation - Chỉ thực thi khi cần thiết

Có thể xử lý vô hạn - Hỗ trợ infinite stream

Chỉ dùng một lần - Sau khi dùng xong phải tạo stream mới

### Tạo Stream
````java
import java.util.*;
import java.util.stream.*;

public class CreateStreamDemo {
    public static void main(String[] args) {
        // 1. Từ Collection
        List<String> list = Arrays.asList("a", "b", "c");
        Stream<String> stream1 = list.stream();
        
        // 2. Từ Array
        String[] array = {"x", "y", "z"};
        Stream<String> stream2 = Arrays.stream(array);
        
        // 3. Từ giá trị cụ thể
        Stream<Integer> stream3 = Stream.of(1, 2, 3, 4, 5);
        
        // 4. Stream vô hạn
        Stream<Integer> infiniteStream = Stream.iterate(0, n -> n + 2);
        
        // 5. Stream ngẫu nhiên
        Stream<Double> randomStream = Stream.generate(Math::random);
        
        // 6. IntStream, LongStream, DoubleStream
        IntStream numbers = IntStream.range(1, 10);  // 1 đến 9
    }
}

````
### Các thao tác trên Stream
Stream có 2 loại thao tác:

#### Intermediate operations (trung gian):
filter, map, sorted... - trả về Stream

#### Terminal operations (kết thúc):
forEach, collect, count... - trả về kết quả cuối cùng

<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>Stream API KHÔNG modify collection gốc!</strong> Streams là <strong>immutable pipeline</strong> - chúng tạo ra kết quả mới mà không thay đổi source. Nếu muốn lưu kết quả, phải dùng <code>.collect()</code>. Và nhớ: <strong>Stream chỉ dùng 1 lần</strong>, không thể reuse sau khi consumed!</p>
</div>

### 1. Filter - Lọc dữ liệu
````java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Lọc các số chẵn
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
System.out.println(evenNumbers);  // [2, 4, 6, 8, 10]

// Lọc các số lớn hơn 5
List<Integer> greaterThan5 = numbers.stream()
    .filter(n -> n > 5)
    .collect(Collectors.toList());
System.out.println(greaterThan5);  // [6, 7, 8, 9, 10]

// Kết hợp nhiều điều kiện
List<Integer> result = numbers.stream()
    .filter(n -> n > 3)
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
System.out.println(result);  // [4, 6, 8, 10]
````
### 2. Map - Biến đổi dữ liệu
```` java
List<String> names = Arrays.asList("an", "binh", "chau");

// Chuyển thành chữ hoa
List<String> upperNames = names.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());
System.out.println(upperNames);  // [AN, BINH, CHAU]

// Tính bình phương
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squares = numbers.stream()
    .map(n -> n * n)
    .collect(Collectors.toList());
System.out.println(squares);  // [1, 4, 9, 16, 25]

// Lấy độ dài chuỗi
List<Integer> lengths = names.stream()
    .map(String::length)
    .collect(Collectors.toList());
System.out.println(lengths);  // [2, 4, 4]
````
### 3. FlatMap - Làm phẳng dữ liệu lồng nhau
````java
List<List<Integer>> nestedList = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5, 6),
    Arrays.asList(7, 8, 9)
);

// Làm phẳng thành một danh sách
List<Integer> flatList = nestedList.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());
System.out.println(flatList);  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Ví dụ thực tế: Lấy tất cả từ từ nhiều câu
List<String> sentences = Arrays.asList(
    "Java is awesome",
    "Stream API is powerful",
    "Lambda makes code clean"
);

List<String> allWords = sentences.stream()
    .flatMap(sentence -> Arrays.stream(sentence.split(" ")))
    .collect(Collectors.toList());
System.out.println(allWords);
// [Java, is, awesome, Stream, API, is, powerful, Lambda, makes, code, clean]
````
### 4. Reduce - Tổng hợp dữ liệu
````java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Tính tổng
int sum = numbers.stream()
    .reduce(0, (a, b) -> a + b);
System.out.println("Tổng: " + sum);  // 15

// Tính tích
int product = numbers.stream()
    .reduce(1, (a, b) -> a * b);
System.out.println("Tích: " + product);  // 120

// Tìm giá trị lớn nhất
Optional<Integer> max = numbers.stream()
    .reduce(Integer::max);
max.ifPresent(value -> System.out.println("Max: " + value));  // 5

// Tìm giá trị nhỏ nhất
Optional<Integer> min = numbers.stream()
    .reduce(Integer::min);
min.ifPresent(value -> System.out.println("Min: " + value));  // 1

// Nối chuỗi
List<String> words = Arrays.asList("Java", "Stream", "API");
String combined = words.stream()
    .reduce("", (a, b) -> a + " " + b);
System.out.println(combined.trim());  // Java Stream API
````
### 5. Sorted - Sắp xếp
```` java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9, 3);

// Sắp xếp tăng dần
List<Integer> sorted = numbers.stream()
    .sorted()
    .collect(Collectors.toList());
System.out.println(sorted);  // [1, 2, 3, 5, 8, 9]

// Sắp xếp giảm dần
List<Integer> reverseSorted = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());
System.out.println(reverseSorted);  // [9, 8, 5, 3, 2, 1]

// Sắp xếp chuỗi theo độ dài
List<String> names = Arrays.asList("An", "Binh", "Chau", "Dung");
List<String> sortedByLength = names.stream()
    .sorted(Comparator.comparing(String::length))
    .collect(Collectors.toList());
System.out.println(sortedByLength);  // [An, Binh, Chau, Dung]
````
### 6. Distinct, Limit, Skip
````java
List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 3, 3, 4, 5, 5);

// Loại bỏ trùng lặp
List<Integer> distinct = numbers.stream()
    .distinct()
    .collect(Collectors.toList());
System.out.println(distinct);  // [1, 2, 3, 4, 5]

// Lấy 3 phần tử đầu
List<Integer> first3 = numbers.stream()
    .limit(3)
    .collect(Collectors.toList());
System.out.println(first3);  // [1, 2, 2]

// Bỏ qua 5 phần tử đầu
List<Integer> skip5 = numbers.stream()
    .skip(5)
    .collect(Collectors.toList());
System.out.println(skip5);  // [3, 4, 5, 5]

// Kết hợp: Bỏ trùng, lấy 3 phần tử
List<Integer> result = numbers.stream()
    .distinct()
    .limit(3)
    .collect(Collectors.toList());
System.out.println(result);  // [1, 2, 3]
````
### Ví dụ thực tế với Class
```` java
class Student {
    private String name;
    private int age;
    private double score;
    private String gender;
    
    public Student(String name, int age, double score, String gender) {
        this.name = name;
        this.age = age;
        this.score = score;
        this.gender = gender;
    }
    
    // Getters
    public String getName() { return name; }
    public int getAge() { return age; }
    public double getScore() { return score; }
    public String getGender() { return gender; }
    
    @Override
    public String toString() {
        return name + " (" + age + " tuổi, điểm: " + score + ")";
    }
}

public class StudentStreamDemo {
    public static void main(String[] args) {
        List<Student> students = Arrays.asList(
            new Student("An", 20, 8.5, "Nam"),
            new Student("Binh", 22, 7.0, "Nam"),
            new Student("Chau", 21, 9.0, "Nữ"),
            new Student("Dung", 23, 6.5, "Nam"),
            new Student("Hoa", 20, 8.0, "Nữ"),
            new Student("Khoa", 22, 5.5, "Nam")
        );
        
        // 1. Lọc sinh viên điểm >= 7.5, lấy tên, sắp xếp
        System.out.println("=== Sinh viên giỏi ===");
        List<String> goodStudents = students.stream()
            .filter(s -> s.getScore() >= 7.5)
            .map(Student::getName)
            .sorted()
            .collect(Collectors.toList());
        System.out.println(goodStudents);  // [An, Chau, Hoa]
        
        // 2. Tính điểm trung bình
        double avgScore = students.stream()
            .mapToDouble(Student::getScore)
            .average()
            .orElse(0.0);
        System.out.println("Điểm TB: " + avgScore);  // 7.42
        
        // 3. Tìm sinh viên có điểm cao nhất
        Optional<Student> topStudent = students.stream()
            .max(Comparator.comparing(Student::getScore));
        topStudent.ifPresent(s -> 
            System.out.println("Sinh viên xuất sắc nhất: " + s)
        );
        
        // 4. Đếm số sinh viên nam
        long maleCount = students.stream()
            .filter(s -> s.getGender().equals("Nam"))
            .count();
        System.out.println("Số sinh viên nam: " + maleCount);  // 4
        
        // 5. Nhóm sinh viên theo độ tuổi
        Map<Integer, List<Student>> byAge = students.stream()
            .collect(Collectors.groupingBy(Student::getAge));
        System.out.println("\n=== Nhóm theo tuổi ===");
        byAge.forEach((age, list) -> {
            System.out.println("Tuổi " + age + ": " + list);
        });
        
        // 6. Phân loại: Đỗ (>= 5.0) và Trượt
        Map<Boolean, List<Student>> passedStudents = students.stream()
            .collect(Collectors.partitioningBy(s -> s.getScore() >= 5.0));
        System.out.println("\n=== Kết quả học tập ===");
        System.out.println("Đỗ: " + passedStudents.get(true).size());
        System.out.println("Trượt: " + passedStudents.get(false).size());
        
        // 7. Tạo danh sách tên, cách nhau bởi dấu phẩy
        String allNames = students.stream()
            .map(Student::getName)
            .collect(Collectors.joining(", ", "[", "]"));
        System.out.println("\nDanh sách: " + allNames);
        
        // 8. Tính tổng điểm của sinh viên nữ
        double femaleScoreSum = students.stream()
            .filter(s -> s.getGender().equals("Nữ"))
            .mapToDouble(Student::getScore)
            .sum();
        System.out.println("Tổng điểm sinh viên nữ: " + femaleScoreSum);
        
        // 9. Có sinh viên nào điểm dưới 6 không?
        boolean hasLowScore = students.stream()
            .anyMatch(s -> s.getScore() < 6.0);
        System.out.println("Có SV điểm yếu: " + hasLowScore);
        
        // 10. Tất cả sinh viên đều trên 18 tuổi?
        boolean allAdult = students.stream()
            .allMatch(s -> s.getAge() >= 18);
        System.out.println("Tất cả đều trưởng thành: " + allAdult);
    }
}
````
### Collectors - Thu thập kết quả
```` java
import java.util.stream.Collectors;

List<String> items = Arrays.asList("apple", "banana", "apple", "orange", "banana", "apple");

// 1. Thành List
List<String> list = items.stream().collect(Collectors.toList());

// 2. Thành Set (loại bỏ trùng)
Set<String> set = items.stream().collect(Collectors.toSet());
System.out.println(set);  // [banana, orange, apple]

// 3. Thành Map với đếm số lần xuất hiện
Map<String, Long> counted = items.stream()
    .collect(Collectors.groupingBy(s -> s, Collectors.counting()));
System.out.println(counted);  // {banana=2, orange=1, apple=3}

// 4. Nối chuỗi
String joined = items.stream()
    .collect(Collectors.joining(", "));
System.out.println(joined);  // apple, banana, apple, orange, banana, apple

// 5. Nối với prefix và suffix
String formatted = items.stream()
    .distinct()
    .collect(Collectors.joining(", ", "Trái cây: [", "]"));
System.out.println(formatted);  // Trái cây: [apple, banana, orange]

// 6. Tính thống kê
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
IntSummaryStatistics stats = numbers.stream()
    .collect(Collectors.summarizingInt(Integer::intValue));
System.out.println("Count: " + stats.getCount());      // 5
System.out.println("Sum: " + stats.getSum());          // 15
System.out.println("Min: " + stats.getMin());          // 1
System.out.println("Max: " + stats.getMax());          // 5
System.out.println("Average: " + stats.getAverage());  // 3.0
````
### Parallel Stream - Xử lý song song
```` java
List<Integer> largeList = new ArrayList<>();
for (int i = 1; i <= 1000000; i++) {
    largeList.add(i);
}

// Stream thông thường
long start1 = System.currentTimeMillis();
long count1 = largeList.stream()
    .filter(n -> n % 2 == 0)
    .count();
long end1 = System.currentTimeMillis();
System.out.println("Sequential: " + (end1 - start1) + "ms");

// Parallel Stream - nhanh hơn với dữ liệu lớn
long start2 = System.currentTimeMillis();
long count2 = largeList.parallelStream()
    .filter(n -> n % 2 == 0)
    .count();
long end2 = System.currentTimeMillis();
System.out.println("Parallel: " + (end2 - start2) + "ms");

System.out.println("Kết quả: " + count1 + " = " + count2);
````
### Lưu ý khi dùng Parallel Stream:

- Chỉ nên dùng với dữ liệu lớn (> 1000 phần tử)

- Không nên dùng với I/O operations

- Cẩn thận với shared mutable state

### Lỗi thường gặp (Common Mistakes)
#### 1. Sử dụng Stream nhiều lần
``` java
// ❌ SAI: Stream chỉ dùng được 1 lần
Stream<Integer> stream = numbers.stream();
stream.forEach(System.out::println);  // OK
stream.forEach(System.out::println);  // Lỗi: stream has already been operated upon

// ✅ ĐÚNG: Tạo stream mới mỗi lần dùng
numbers.stream().forEach(System.out::println);
numbers.stream().filter(n -> n > 5).forEach(System.out::println);
````
#### 2. Quên collect() hoặc terminal operation
```` java
// ❌ SAI: Chỉ có intermediate operation, không có terminal operation
numbers.stream()
    .filter(n -> n > 5)
    .map(n -> n * 2);  // Không làm gì cả!

// ✅ ĐÚNG: Phải có terminal operation
List<Integer> result = numbers.stream()
    .filter(n -> n > 5)
    .map(n -> n * 2)
    .collect(Collectors.toList());  // Hoặc forEach, count, etc.
````
#### 3. Thay đổi dữ liệu trong lambda
```` java
// ❌ SAI: Không nên thay đổi biến bên ngoài
List<Integer> result = new ArrayList<>();
numbers.stream()
    .filter(n -> n > 5)
    .forEach(n -> result.add(n * 2));  // Side effect!

// ✅ ĐÚNG: Dùng map và collect
List<Integer> result = numbers.stream()
    .filter(n -> n > 5)
    .map(n -> n * 2)
    .collect(Collectors.toList());
````
#### 4. Nhầm lẫn map() và flatMap()
````java

List<List<Integer>> nested = Arrays.asList(
    Arrays.asList(1, 2),
    Arrays.asList(3, 4)
);

// ❌ SAI: map() sẽ tạo Stream<Stream<Integer>>
Stream<Stream<Integer>> wrong = nested.stream()
    .map(List::stream);  // Không làm phẳng được!

// ✅ ĐÚNG: Dùng flatMap()
List<Integer> flat = nested.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());  // [1, 2, 3, 4]
````
### Best Practices - Cách viết tốt
#### 1. Ưu tiên method reference
```` java
// ❌ Không tối ưu
names.stream().map(s -> s.toUpperCase())

// ✅ Tốt hơn
names.stream().map(String::toUpperCase)

// ❌ Không tối ưu
numbers.stream().forEach(n -> System.out.println(n))

// ✅ Tốt hơn
numbers.stream().forEach(System.out::println)
````
#### 2. Tránh quá nhiều chaining
```` java
// ❌ Khó đọc
List<String> result = students.stream().filter(s -> s.getScore() >= 7.5).map(Student::getName).sorted().limit(5).collect(Collectors.toList());

// ✅ Dễ đọc hơn
List<String> result = students.stream()
    .filter(s -> s.getScore() >= 7.5)
    .map(Student::getName)
    .sorted()
    .limit(5)
    .collect(Collectors.toList());
````
#### 3. Sử dụng Optional đúng cách
```` java
// ❌ SAI
Optional<Student> student = students.stream()
    .filter(s -> s.getName().equals("An"))
    .findFirst();
if (student.get() != null) {  // Có thể gây lỗi!
    System.out.println(student.get());
}

// ✅ ĐÚNG
students.stream()
    .filter(s -> s.getName().equals("An"))
    .findFirst()
    .ifPresent(System.out::println);

// Hoặc với giá trị mặc định
String name = students.stream()
    .filter(s -> s.getScore() > 9.0)
    .map(Student::getName)
    .findFirst()
    .orElse("Không có");
````
---

## 🐛 Lỗi thường gặp với Lambda & Stream API

### ❌ Lỗi 1: Reuse Stream sau khi consumed

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Stream Has Already Been Operated Upon</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Stream chỉ có thể dùng <strong>1 LẦN DUY NHẤT</strong>. Sau khi terminal operation (collect, forEach, count...), stream bị closed!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - Stream đã consumed!
Stream<Integer> stream = List.of(1, 2, 3).stream();
long count = stream.count();  // Terminal operation

// Lỗi: Stream has already been operated upon or closed
stream.forEach(System.out::println);  // ❌ Error!
```

**Lỗi:**
```
IllegalStateException: stream has already been operated upon or closed
```

**Cách fix:**
```java
// ✅ ĐÚNG - Tạo stream mới mỗi lần dùng
List<Integer> numbers = List.of(1, 2, 3);

long count = numbers.stream().count();
numbers.stream().forEach(System.out::println);

// ✅ HOẶC - Dùng Supplier để tạo stream nhiều lần
Supplier<Stream<Integer>> streamSupplier = 
    () -> List.of(1, 2, 3).stream();

long count = streamSupplier.get().count();
streamSupplier.get().forEach(System.out::println);
```

---

### ❌ Lỗi 2: Modify variable trong Lambda

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Variable Must Be Final or Effectively Final</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Lambda chỉ có thể access biến <strong>final hoặc effectively final</strong> từ outer scope!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - sum không phải effectively final
int sum = 0;
List<Integer> numbers = List.of(1, 2, 3, 4, 5);

numbers.forEach(n -> {
    sum += n;  // ❌ Compile error!
});
```

**Lỗi:**
```
error: local variables referenced from a lambda expression must be final or effectively final
```

**Cách fix:**
```java
// ✅ ĐÚNG - Cách 1: Dùng Stream reduce
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
int sum = numbers.stream()
    .reduce(0, Integer::sum);

// ✅ ĐÚNG - Cách 2: Dùng wrapper class
class Counter {
    int value = 0;
}
Counter counter = new Counter();
numbers.forEach(n -> counter.value += n);

// ✅ ĐÚNG - Cách 3: Dùng AtomicInteger
AtomicInteger sum = new AtomicInteger(0);
numbers.forEach(n -> sum.addAndGet(n));
```

**💡 Best Practice:** Prefer functional style với `reduce()` thay vì mutation!

---

### ❌ Lỗi 3: Quên collect() kết quả

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Stream Pipeline Không Thực Thi</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Stream là <strong>lazy evaluation</strong> - không có terminal operation thì không chạy gì cả!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - Không có terminal operation!
List<Integer> numbers = List.of(1, 2, 3, 4, 5);

numbers.stream()
    .filter(n -> n > 2)
    .map(n -> n * 2);
// Không làm gì cả! Stream pipeline không execute

System.out.println(numbers);  // [1, 2, 3, 4, 5] - không thay đổi!
```

**Tại sao không chạy?**
- Stream operations là **lazy** (trừ terminal operations)
- Không có `collect()`, `forEach()`, `count()`... → không execute
- Stream không modify collection gốc

**Cách fix:**
```java
// ✅ ĐÚNG - Thêm terminal operation
List<Integer> result = numbers.stream()
    .filter(n -> n > 2)
    .map(n -> n * 2)
    .collect(Collectors.toList());  // Terminal operation!

System.out.println(result);  // [6, 8, 10]

// ✅ HOẶC - forEach để side effect
numbers.stream()
    .filter(n -> n > 2)
    .map(n -> n * 2)
    .forEach(System.out::println);  // Terminal operation!
```

---

### ❌ Lỗi 4: Nhầm map() và flatMap()

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">map() vs flatMap()</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Dùng <code>map()</code> với nested collections tạo ra <code>Stream&lt;Stream&lt;T&gt;&gt;</code> thay vì <code>Stream&lt;T&gt;</code>!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - Dùng map() cho nested list
List<List<Integer>> nested = List.of(
    List.of(1, 2),
    List.of(3, 4),
    List.of(5, 6)
);

// Kiểu: Stream<Stream<Integer>> (không phải Stream<Integer>!)
Stream<Stream<Integer>> result = nested.stream()
    .map(list -> list.stream());  // ❌ Nested stream!
```

**Cách fix:**
```java
// ✅ ĐÚNG - Dùng flatMap() để flatten
List<Integer> flattened = nested.stream()
    .flatMap(list -> list.stream())  // Flatten
    .collect(Collectors.toList());

System.out.println(flattened);  // [1, 2, 3, 4, 5, 6]

// ✅ Rule of thumb:
// map():     T -> R              (1-to-1)
// flatMap(): T -> Stream<R>      (1-to-many, then flatten)
```
---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** Lambda Expression là gì? Syntax như thế nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Lambda Expression:</strong> Anonymous function (hàm không tên) dùng để implement functional interface</p>
    <p style="margin: 0 0 10px 0;"><strong>Syntax:</strong></p>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 0;"><code>// Không parameters
() -> expression
() -> { statements; }

// 1 parameter
x -> expression
(x) -> expression

// Nhiều parameters
(x, y) -> expression
(x, y) -> { statements; }</code></pre>
  </div>
</details>

**Câu 2:** Functional Interface là gì? Ví dụ built-in interfaces?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Functional Interface:</strong> Interface có <strong>ĐÚNG 1</strong> abstract method (SAM - Single Abstract Method)</p>
    <p style="margin: 0 0 10px 0;"><strong>Built-in interfaces:</strong></p>
    <ul style="margin: 0;">
      <li><code>Predicate&lt;T&gt;</code>: T → boolean (test condition)</li>
      <li><code>Function&lt;T,R&gt;</code>: T → R (transform)</li>
      <li><code>Consumer&lt;T&gt;</code>: T → void (side effect)</li>
      <li><code>Supplier&lt;T&gt;</code>: () → T (provide value)</li>
      <li><code>BiFunction&lt;T,U,R&gt;</code>: (T, U) → R</li>
    </ul>
  </div>
</details>

**Câu 3:** map() vs flatMap() - Khác nhau gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Tiêu chí</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">map()</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">flatMap()</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Transformation</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">1-to-1</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">1-to-many</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Input → Output</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">T → R</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">T → Stream&lt;R&gt;</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Kết quả</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Stream&lt;R&gt;</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Stream&lt;R&gt; (flattened)</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Use case</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Transform elements</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Flatten nested structures</td>
      </tr>
    </table>
  </div>
</details>

**Câu 4:** Intermediate vs Terminal Operations?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🔗 Intermediate Operations (lazy):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Return Stream → có thể chain tiếp</li>
      <li>Không execute ngay (lazy evaluation)</li>
      <li>Ví dụ: <code>filter()</code>, <code>map()</code>, <code>flatMap()</code>, <code>distinct()</code>, <code>sorted()</code>, <code>limit()</code>, <code>skip()</code></li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🎯 Terminal Operations (eager):</strong></p>
    <ul style="margin: 0;">
      <li>Trigger execution của toàn bộ pipeline</li>
      <li>Return kết quả (không phải Stream)</li>
      <li>Ví dụ: <code>collect()</code>, <code>forEach()</code>, <code>count()</code>, <code>reduce()</code>, <code>anyMatch()</code>, <code>findFirst()</code></li>
    </ul>
  </div>
</details>

**Câu 5:** Method Reference là gì? Các loại nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>Method Reference:</strong> Cú pháp ngắn gọn cho lambda khi chỉ gọi 1 method</p>
    <p style="margin: 0 0 10px 0;"><strong>4 loại:</strong></p>
    <ol style="margin: 0;">
      <li><strong>Static method:</strong> <code>ClassName::staticMethod</code> → <code>Integer::parseInt</code></li>
      <li><strong>Instance method (object):</strong> <code>instance::method</code> → <code>System.out::println</code></li>
      <li><strong>Instance method (class):</strong> <code>ClassName::method</code> → <code>String::toUpperCase</code></li>
      <li><strong>Constructor:</strong> <code>ClassName::new</code> → <code>ArrayList::new</code></li>
    </ol>
  </div>
</details>

</div>

### Bài tập thực hành
#### Bài 1: Xử lý danh sách số
```` java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9, 3, 7, 4, 6, 10);

// Yêu cầu:
// 1. Lọc các số chẵn
// 2. Nhân đôi mỗi số
// 3. Sắp xếp giảm dần
// 4. Lấy 5 số đầu tiên
// 5. In ra kết quả

// Đáp án:
List<Integer> result = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .sorted(Comparator.reverseOrder())
    .limit(5)
    .collect(Collectors.toList());
System.out.println(result);  // [20, 16, 12, 8, 4]
````
#### Bài 2: Đếm tần suất từ
```` java
List<String> words = Arrays.asList(
    "java", "python", "java", "javascript", 
    "java", "python", "c++", "javascript"
);

// Yêu cầu: Tạo Map<String, Long> đếm số lần xuất hiện

// Đáp án:
Map<String, Long> frequency = words.stream()
    .collect(Collectors.groupingBy(w -> w, Collectors.counting()));
System.out.println(frequency);
// {java=3, python=2, javascript=2, c++=1}
````
#### Bài 3: Xử lý danh sách sản phẩm
```` java
class Product {
    private String name;
    private String category;
    private double price;
    private int quantity;
    
    public Product(String name, String category, double price, int quantity) {
        this.name = name;
        this.category = category;
        this.price = price;
        this.quantity = quantity;
    }
    
    public String getName() { return name; }
    public String getCategory() { return category; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
    public double getTotalValue() { return price * quantity; }
    
    @Override
    public String toString() {
        return name + " (" + category + ", " + price + "đ, SL: " + quantity + ")";
    }
}

public class ProductExercise {
    public static void main(String[] args) {
        List<Product> products = Arrays.asList(
            new Product("Laptop Dell", "Electronics", 15000000, 5),
            new Product("iPhone 15", "Electronics", 25000000, 3),
            new Product("Áo thun", "Fashion", 200000, 50),
            new Product("Quần jean", "Fashion", 500000, 30),
            new Product("Tivi Samsung", "Electronics", 12000000, 8),
            new Product("Giày Nike", "Fashion", 2000000, 15),
            new Product("Tai nghe AirPods", "Electronics", 5000000, 10)
        );
        
        // 1. Tìm sản phẩm đắt nhất
        Optional<Product> mostExpensive = products.stream()
            .max(Comparator.comparing(Product::getPrice));
        mostExpensive.ifPresent(p -> 
            System.out.println("Sản phẩm đắt nhất: " + p)
        );
        
        // 2. Tính tổng giá trị kho hàng theo danh mục
        Map<String, Double> totalByCategory = products.stream()
            .collect(Collectors.groupingBy(
                Product::getCategory,
                Collectors.summingDouble(Product::getTotalValue)
            ));
        System.out.println("\nTổng giá trị theo danh mục:");
        totalByCategory.forEach((cat, total) -> 
            System.out.println(cat + ": " + total + "đ")
        );
        
        // 3. Tìm top 3 sản phẩm có giá trị kho cao nhất
        List<Product> top3 = products.stream()
            .sorted(Comparator.comparing(Product::getTotalValue).reversed())
            .limit(3)
            .collect(Collectors.toList());
        System.out.println("\nTop 3 sản phẩm giá trị cao:");
        top3.forEach(System.out::println);
        
        // 4. Đếm số sản phẩm theo danh mục
        Map<String, Long> countByCategory = products.stream()
            .collect(Collectors.groupingBy(
                Product::getCategory,
                Collectors.counting()
            ));
        System.out.println("\nSố lượng sản phẩm theo danh mục:");
        countByCategory.forEach((cat, count) -> 
            System.out.println(cat + ": " + count + " sản phẩm")
        );
        
        // 5. Lấy danh sách tên sản phẩm Electronics, giá > 10 triệu
        List<String> expensiveElectronics = products.stream()
            .filter(p -> p.getCategory().equals("Electronics"))
            .filter(p -> p.getPrice() > 10000000)
            .map(Product::getName)
            .collect(Collectors.toList());
        System.out.println("\nĐiện tử cao cấp: " + expensiveElectronics);
        
        // 6. Tính tổng số lượng tất cả sản phẩm
        int totalQuantity = products.stream()
            .mapToInt(Product::getQuantity)
            .sum();
        System.out.println("\nTổng số lượng: " + totalQuantity + " sản phẩm");
        
        // 7. Giá trung bình của sản phẩm Fashion
        double avgFashionPrice = products.stream()
            .filter(p -> p.getCategory().equals("Fashion"))
            .mapToDouble(Product::getPrice)
            .average()
            .orElse(0.0);
        System.out.println("Giá TB Fashion: " + avgFashionPrice + "đ");
    }
}
````
#### Bài 4: Xử lý chuỗi văn bản
````java
String text = "Java Stream API makes functional programming easy. " +
              "Lambda expressions help write cleaner code. " +
              "Java 8 introduced many powerful features.";

// Yêu cầu:
// 1. Tách thành các từ
// 2. Chuyển thành chữ thường
// 3. Loại bỏ từ trùng lặp
// 4. Sắp xếp theo thứ tự alphabet
// 5. Đếm tổng số từ unique

// Đáp án:
List<String> words = Arrays.stream(text.split("\\s+"))
    .map(word -> word.replaceAll("[^a-zA-Z]", "").toLowerCase())
    .filter(word -> !word.isEmpty())
    .distinct()
    .sorted()
    .collect(Collectors.toList());

System.out.println("Các từ unique: " + words);
System.out.println("Tổng số từ unique: " + words.size());

// Đếm từ xuất hiện nhiều nhất
Map<String, Long> wordFrequency = Arrays.stream(text.split("\\s+"))
    .map(word -> word.replaceAll("[^a-zA-Z]", "").toLowerCase())
    .filter(word -> !word.isEmpty())
    .collect(Collectors.groupingBy(w -> w, Collectors.counting()));

wordFrequency.entrySet().stream()
    .max(Map.Entry.comparingByValue())
    .ifPresent(entry -> 
        System.out.println("Từ xuất hiện nhiều nhất: " + entry.getKey() + 
                         " (" + entry.getValue() + " lần)")
    );
````
#### Bài 5: Tìm số nguyên tố
```java
// Yêu cầu: Tìm các số nguyên tố từ 1 đến 100

public static boolean isPrime(int n) {
    if (n < 2) return false;
    return IntStream.rangeClosed(2, (int) Math.sqrt(n))
        .noneMatch(i -> n % i == 0);
}

public static void main(String[] args) {
    List<Integer> primes = IntStream.rangeClosed(1, 100)
        .filter(ProductExercise::isPrime)
        .boxed()
        .collect(Collectors.toList());
    
    System.out.println("Các số nguyên tố từ 1-100:");
    System.out.println(primes);
    System.out.println("Tổng cộng: " + primes.size() + " số");
    
    // Tính tổng các số nguyên tố
    int sum = primes.stream()
        .mapToInt(Integer::intValue)
        .sum();
    System.out.println("Tổng các số nguyên tố: " + sum);
}
```
#### Bài 6: Xử lý danh sách giao dịch
```java
class Transaction {
    private String id;
    private String type; // "BUY" hoặc "SELL"
    private double amount;
    private String date;
    
    public Transaction(String id, String type, double amount, String date) {
        this.id = id;
        this.type = type;
        this.amount = amount;
        this.date = date;
    }
    
    public String getId() { return id; }
    public String getType() { return type; }
    public double getAmount() { return amount; }
    public String getDate() { return date; }
    
    @Override
    public String toString() {
        return id + ": " + type + " - " + amount + "đ (" + date + ")";
    }
}

public class TransactionAnalysis {
    public static void main(String[] args) {
        List<Transaction> transactions = Arrays.asList(
            new Transaction("T001", "BUY", 1000000, "2024-10-01"),
            new Transaction("T002", "SELL", 500000, "2024-10-02"),
            new Transaction("T003", "BUY", 2000000, "2024-10-03"),
            new Transaction("T004", "BUY", 1500000, "2024-10-04"),
            new Transaction("T005", "SELL", 800000, "2024-10-05"),
            new Transaction("T006", "SELL", 1200000, "2024-10-06"),
            new Transaction("T007", "BUY", 3000000, "2024-10-07")
        );
        
        // 1. Tính tổng số tiền BUY
        double totalBuy = transactions.stream()
            .filter(t -> t.getType().equals("BUY"))
            .mapToDouble(Transaction::getAmount)
            .sum();
        System.out.println("Tổng mua: " + totalBuy + "đ");
        
        // 2. Tính tổng số tiền SELL
        double totalSell = transactions.stream()
            .filter(t -> t.getType().equals("SELL"))
            .mapToDouble(Transaction::getAmount)
            .sum();
        System.out.println("Tổng bán: " + totalSell + "đ");
        
        // 3. Số dư (BUY - SELL)
        System.out.println("Số dư: " + (totalBuy - totalSell) + "đ");
        
        // 4. Giao dịch lớn nhất
        Optional<Transaction> largest = transactions.stream()
            .max(Comparator.comparing(Transaction::getAmount));
        largest.ifPresent(t -> 
            System.out.println("Giao dịch lớn nhất: " + t)
        );
        
        // 5. Nhóm theo loại giao dịch
        Map<String, List<Transaction>> byType = transactions.stream()
            .collect(Collectors.groupingBy(Transaction::getType));
        
        System.out.println("\nSố giao dịch theo loại:");
        byType.forEach((type, list) -> 
            System.out.println(type + ": " + list.size() + " giao dịch")
        );
        
        // 6. Giá trị trung bình mỗi giao dịch
        double avgAmount = transactions.stream()
            .mapToDouble(Transaction::getAmount)
            .average()
            .orElse(0.0);
        System.out.println("\nGiá trị TB giao dịch: " + avgAmount + "đ");
        
        // 7. Các giao dịch > 1 triệu
        List<Transaction> largeTransactions = transactions.stream()
            .filter(t -> t.getAmount() > 1000000)
            .collect(Collectors.toList());
        System.out.println("\nGiao dịch > 1 triệu:");
        largeTransactions.forEach(System.out::println);
    }
}
````
## Ví dụ nâng cao

### 1. Custom Collector
```java
// Tạo collector riêng để nối chuỗi với số thứ tự
List<String> names = Arrays.asList("An", "Binh", "Chau", "Dung");

String numbered = IntStream.range(0, names.size())
    .mapToObj(i -> (i + 1) + ". " + names.get(i))
    .collect(Collectors.joining("\n"));

System.out.println(numbered);
// Output:
// 1. An
// 2. Binh
// 3. Chau
// 4. Dung
````
### 2. Tìm phần tử thứ N
```java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9, 3, 7, 4, 6);

// Tìm số lớn thứ 3
Optional<Integer> thirdLargest = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .skip(2)
    .findFirst();
thirdLargest.ifPresent(n -> 
    System.out.println("Số lớn thứ 3: " + n)
);  // 7
````
### 3. Peek - Debug Stream
```java
List<Integer> result = numbers.stream()
    .peek(n -> System.out.println("Trước filter: " + n))
    .filter(n -> n > 5)
    .peek(n -> System.out.println("Sau filter: " + n))
    .map(n -> n * 2)
    .peek(n -> System.out.println("Sau map: " + n))
    .collect(Collectors.toList());
```

### 4. Infinite Stream
```java
// Tạo dãy Fibonacci
Stream.iterate(new int[]{0, 1}, f -> new int[]{f[1], f[0] + f[1]})
    .limit(10)
    .map(f -> f[0])
    .forEach(System.out::println);
// Output: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34

// Tạo số ngẫu nhiên
Stream.generate(Math::random)
    .limit(5)
    .forEach(System.out::println);
```

### 5. Xử lý Map với Stream
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("An", 85);
scores.put("Binh", 70);
scores.put("Chau", 90);
scores.put("Dung", 65);

// Lọc điểm >= 75
Map<String, Integer> passed = scores.entrySet().stream()
    .filter(entry -> entry.getValue() >= 75)
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
System.out.println(passed);  // {An=85, Chau=90}

// Sắp xếp theo điểm giảm dần
scores.entrySet().stream()
    .sorted(Map.Entry.comparingByValue(Comparator.reverseOrder()))
    .forEach(entry -> 
        System.out.println(entry.getKey() + ": " + entry.getValue())
    );

// Tìm người có điểm cao nhất
scores.entrySet().stream()
    .max(Map.Entry.comparingByValue())
    .ifPresent(entry -> 
        System.out.println("Cao nhất: " + entry.getKey() + " - " + entry.getValue())
    );
```

## Tips & Tricks

### 1. Tối ưu hiệu năng
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// ❌ Không tối ưu - filter 2 lần
numbers.stream()
    .filter(n -> n > 3)
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

// ✅ Tối ưu - filter 1 lần
numbers.stream()
    .filter(n -> n > 3 && n % 2 == 0)
    .collect(Collectors.toList());

// ❌ Không tối ưu - tạo object không cần thiết
numbers.stream()
    .map(n -> n * 2)
    .mapToInt(Integer::intValue)
    .sum();

// ✅ Tối ưu - dùng mapToInt trực tiếp
numbers.stream()
    .mapToInt(n -> n * 2)
    .sum();
```

### 2. Short-circuit operations
```java
// findFirst() và findAny() - dừng khi tìm thấy
Optional<Integer> first = numbers.stream()
    .filter(n -> n > 5)
    .findFirst();  // Dừng ngay khi tìm thấy

// anyMatch(), allMatch(), noneMatch() - dừng sớm
boolean hasEven = numbers.stream()
    .anyMatch(n -> n % 2 == 0);  // Dừng khi tìm thấy số chẵn đầu tiên

// limit() - chỉ xử lý N phần tử đầu
numbers.stream()
    .filter(n -> n > 0)
    .limit(5)  // Chỉ lấy 5 phần tử đầu
    .collect(Collectors.toList());
```

### 3. Combining Multiple Predicates
```java
Predicate<Integer> isEven = n -> n % 2 == 0;
Predicate<Integer> greaterThan5 = n -> n > 5;
Predicate<Integer> lessThan20 = n -> n < 20;

// Kết hợp các điều kiện
List<Integer> result = numbers.stream()
    .filter(isEven.and(greaterThan5).and(lessThan20))
    .collect(Collectors.toList());

// Hoặc dùng or()
Predicate<Integer> isSmallOrLarge = n -> n < 3 || n > 8;
```

### 4. Xử lý null an toàn
```java
List<String> names = Arrays.asList("An", null, "Binh", null, "Chau");

// Loại bỏ null
List<String> nonNull = names.stream()
    .filter(Objects::nonNull)
    .collect(Collectors.toList());
System.out.println(nonNull);  // [An, Binh, Chau]

// Hoặc dùng Optional
names.stream()
    .filter(Objects::nonNull)
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

## So sánh: Trước và sau Stream API

### Ví dụ 1: Lọc và transform
```java
List<String> names = Arrays.asList("an", "binh", "chau", "dung", "hoa");

// ❌ Cách cũ - dài dòng
List<String> result = new ArrayList<>();
for (String name : names) {
    if (name.length() > 2) {
        result.add(name.toUpperCase());
    }
}
Collections.sort(result);

// ✅ Với Stream - ngắn gọn và rõ ràng
List<String> result = names.stream()
    .filter(name -> name.length() > 2)
    .map(String::toUpperCase)
    .sorted()
    .collect(Collectors.toList());
```

### Ví dụ 2: Tính tổng có điều kiện
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// ❌ Cách cũ
int sum = 0;
for (int n : numbers) {
    if (n % 2 == 0) {
        sum += n;
    }
}

// ✅ Với Stream
int sum = numbers.stream()
    .filter(n -> n % 2 == 0)
    .mapToInt(Integer::intValue)
    .sum();
```

### Ví dụ 3: Nhóm dữ liệu
```java
List<Student> students = getStudents();

// ❌ Cách cũ - phức tạp
Map<Integer, List<Student>> byAge = new HashMap<>();
for (Student s : students) {
    int age = s.getAge();
    if (!byAge.containsKey(age)) {
        byAge.put(age, new ArrayList<>());
    }
    byAge.get(age).add(s);
}

// ✅ Với Stream - một dòng!
Map<Integer, List<Student>> byAge = students.stream()
    .collect(Collectors.groupingBy(Student::getAge));
```

## Kết luận

Lambda expression và Stream API là những tính năng vô cùng mạnh mẽ của Java hiện đại. Chúng giúp:

✅ **Code ngắn gọn hơn**: Giảm thiểu boilerplate code đáng kể

✅ **Dễ đọc và bảo trì**: Code theo phong cách declarative, rõ ràng hơn imperative

✅ **Ít lỗi hơn**: Immutability và functional programming giảm side effects

✅ **Hiệu năng tốt**: Hỗ trợ xử lý song song với Parallel Stream

✅ **Linh hoạt**: Dễ dàng kết hợp các operations

**Lời khuyên:**
- Bắt đầu với các ví dụ đơn giản
- Thực hành thường xuyên với các bài tập
- Đọc code của người khác để học thêm patterns
- Không lạm dụng - đôi khi for loop truyền thống vẫn tốt hơn
- Luôn chú ý performance khi xử lý dữ liệu lớn

## Tài liệu tham khảo

- [Oracle Java Documentation - Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)
- [Oracle Java Documentation - Stream API](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)
- [Baeldung - Java 8 Stream Tutorial](https://www.baeldung.com/java-8-streams)
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai2" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">☕</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Java Collections Framework</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">ArrayList, HashMap - nền tảng để xử lý Stream</p>
  </div>
</a>

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">So sánh Functional Programming Java vs JavaScript</p>
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




