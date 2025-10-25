---
title: "Collections Framework trong Java"
date: 2025-10-10T02:00:00Z
draft: false
---

<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#giới-thiệu">Giới thiệu</a></li>
    <li><a href="#tại-sao-cần-collections-framework">Tại sao cần Collections Framework?</a></li>
    <li><a href="#kiến-trúc-collections-framework">Kiến trúc Collections Framework</a></li>
    <li><a href="#list---danh-sách-có-thứ-tự"> LIST – Danh sách có thứ tự</a>
      <ul>
        <li><a href="#41-arraylist">4.1 ArrayList</a></li>
        <li><a href="#42-linkedlist">4.2 LinkedList</a></li>
        <li><a href="#43-vector-và-stack">4.3 Vector và Stack</a></li>
      </ul>
    </li>
    <li><a href="#set---tập-hợp-không-trùng-lặp"> SET – Tập hợp không trùng lặp</a>
      <ul>
        <li><a href="#51-hashset">5.1 HashSet</a></li>
        <li><a href="#52-linkedhashset">5.2 LinkedHashSet</a></li>
        <li><a href="#53-treeset">5.3 TreeSet</a></li>
      </ul>
    </li>
    <li><a href="#queue---hàng-đợi"> QUEUE – Hàng đợi</a>
      <ul>
        <li><a href="#31-priorityqueue">6.1 PriorityQueue</a></li>
        <li><a href="#32-arraydeque">6.2 ArrayDeque</a></li>
      </ul>
    </li>
    <li><a href="#map---ánh-xạ-key-value"> MAP – Ánh xạ Key-Value</a>
      <ul>
        <li><a href="#71-hashmap">7.1 HashMap</a></li>
        <li><a href="#72-linkedhashmap">7.2 LinkedHashMap</a></li>
        <li><a href="#73-treemap">7.3 TreeMap</a></li>
      </ul>
    </li>
    <li><a href="#ví-dụ-thực-tế">Ví dụ thực tế</a>
      <ul>
        <li><a href="#ví-dụ-1-quản-lý-sinh-viên">Ví dụ 1: Quản lý sinh viên</a></li>
        <li><a href="#ví-dụ-2-giỏ-hàng-mua-sắm">Ví dụ 2: Giỏ hàng mua sắm</a></li>
      </ul>
    </li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## Giới thiệu
Collections Framework là một kiến trúc thống nhất để biểu diễn và thao tác với các tập hợp dữ liệu trong Java. Nó cung cấp các cấu trúc dữ liệu (data structures) và thuật toán (algorithms) mạnh mẽ, giúp lập trình viên làm việc với dữ liệu một cách hiệu quả và dễ dàng.
Trước khi có Collections Framework, Java chỉ có các class như Vector, Stack, Hashtable, và Array. Collections Framework ra đời từ Java 1.2 đã chuẩn hóa cách làm việc với tập hợp dữ liệu.
## Tại sao cần Collections Framework?
### 1. Kích thước linh động: Array có kích thước cố định, Collections tự động mở rộng khi cần.
```java
// Array - Kích thước cố định
String[] names = new String[5];
names[0] = "An";
// Không thể thêm phần tử thứ 6!

// ArrayList - Tự động mở rộng
List<String> names = new ArrayList<>();
names.add("An");
names.add("Binh");
// Có thể thêm bao nhiêu tùy thích!
````
### 2. API phong phú: Collections cung cấp nhiều method tiện ích sẵn có.
```java
// Với Array - Phải tự viết code
for (int i = 0; i < array.length; i++) {
    if (array[i].equals("An")) {
        // found
    }
}

// Với ArrayList - Chỉ 1 dòng
boolean found = list.contains("An");
````
### 3. Hiệu năng tối ưu: Mỗi collection được tối ưu cho từng mục đích cụ thể.
```java
// HashSet - Tìm kiếm cực nhanh O(1)
Set<String> set = new HashSet<>();
boolean exists = set.contains("An");  // Rất nhanh!

// TreeSet - Tự động sắp xếp
Set<Integer> sorted = new TreeSet<>();
sorted.add(5);
sorted.add(1);
sorted.add(3);
System.out.println(sorted);  // [1, 3, 5]
````
### 4. Type safety với Generics: Tránh lỗi runtime do cast sai kiểu.
```` java
// Trước khi có Generics
List list = new ArrayList();
list.add("An");
String name = (String) list.get(0);  // Phải cast thủ công

// Với Generics
List<String> list = new ArrayList<>();
list.add("An");
String name = list.get(0);  // Không cần cast, an toàn hơn
````
### 5. Thread-safe options: Có các collection hỗ trợ đa luồng.
```` java
// Thread-safe collections
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();
````
## Kiến trúc Collections Framework
### Cấu trúc phân cấp
Collections Framework được tổ chức thành nhiều cấp với các interface và class cụ thể:
### Interface gốc:
Collection: Interface chung nhất cho các tập hợp phần tử đơn

Map: Interface riêng biệt cho cấu trúc key-value (không kế thừa Collection)

Các interface con của Collection:

List: Danh sách có thứ tự, cho phép trùng lặp. Các class: ArrayList, LinkedList, Vector, Stack

Set: Tập hợp không trùng lặp, không có thứ tự index. Các class: HashSet, LinkedHashSet, TreeSet

Queue: Hàng đợi FIFO (First In First Out). Các class: PriorityQueue, ArrayDeque, LinkedList

Các class Map:

HashMap: Map dựa trên hash table, nhanh nhất nhưng không có thứ tự
LinkedHashMap: Giữ thứ tự insertion
TreeMap: Map được sắp xếp theo key
Hashtable: Phiên bản cũ, thread-safe nhưng chậm

Khi nào dùng loại nào?
Chọn List khi:

Cần truy cập phần tử theo vị trí (index)
Cho phép phần tử trùng lặp
Quan tâm đến thứ tự

Chọn Set khi:

Không muốn phần tử trùng lặp
Cần kiểm tra tồn tại nhanh
Không quan tâm thứ tự hoặc cần tự động sắp xếp

Chọn Queue khi:

Xử lý theo thứ tự FIFO
Cần priority queue
Implement task scheduling

Chọn Map khi:

Lưu trữ theo cặp key-value
Cần tra cứu nhanh theo key
Mỗi key là duy nhất

## LIST - Danh sách có thứ tự
List là một collection có thứ tự (ordered), cho phép các phần tử trùng lặp và có thể truy cập theo index.

### 4.1 ArrayList
ArrayList là implementation phổ biến nhất của List, sử dụng mảng động bên trong.
Đặc điểm:

 Truy cập nhanh theo index: O(1)

 Duyệt qua các phần tử nhanh

 Tốn ít bộ nhớ

 Chèn/xóa ở giữa chậm: O(n)

 Không thread-safe

Khi nào dùng ArrayList:

Truy cập ngẫu nhiên nhiều (get theo index)

Thêm/xóa ở cuối list

Không cần thread-safe

Đọc nhiều hơn ghi

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Khởi tạo ArrayList với capacity ban đầu nếu biết trước số lượng phần tử: <code style="background: rgba(255,255,255,0.2); padding: 2px 6px; border-radius: 4px;">new ArrayList<>(100)</code>. Điều này tránh resize nhiều lần và cải thiện performance đáng kể!</p>
</div>

```java
import java.util.*;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Tạo ArrayList
        List<String> fruits = new ArrayList<>();
        
        // Thêm phần tử
        fruits.add("Táo");
        fruits.add("Chuối");
        fruits.add("Cam");
        fruits.add("Dưa hấu");
        System.out.println("Danh sách: " + fruits);
        
        // Thêm vào vị trí cụ thể
        fruits.add(1, "Xoài");
        System.out.println("Sau khi thêm: " + fruits);
        
        // Truy cập theo index
        String first = fruits.get(0);
        System.out.println("Phần tử đầu: " + first);
        
        // Thay đổi phần tử
        fruits.set(0, "Táo Đỏ");
        System.out.println("Sau khi sửa: " + fruits);
        
        // Xóa phần tử
        fruits.remove("Chuối");  // Xóa theo object
        fruits.remove(0);         // Xóa theo index
        System.out.println("Sau khi xóa: " + fruits);
        
        // Kiểm tra tồn tại
        boolean hasCam = fruits.contains("Cam");
        System.out.println("Có Cam không? " + hasCam);
        
        // Kích thước
        int size = fruits.size();
        System.out.println("Số lượng: " + size);
        
        // Duyệt qua các phần tử
        System.out.println("\n=== Các cách duyệt ===");
        
        // Cách 1: For loop truyền thống
        for (int i = 0; i < fruits.size(); i++) {
            System.out.println(i + ". " + fruits.get(i));
        }
        
        // Cách 2: Enhanced for loop
        for (String fruit : fruits) {
            System.out.println("- " + fruit);
        }
        
        // Cách 3: Iterator
        Iterator<String> iterator = fruits.iterator();
        while (iterator.hasNext()) {
            System.out.println("* " + iterator.next());
        }
        
        // Cách 4: forEach với Lambda (Java 8+)
        fruits.forEach(fruit -> System.out.println("> " + fruit));
        
        // Cách 5: Stream API (Java 8+)
        fruits.stream().forEach(System.out::println);
        
        // Sắp xếp
        Collections.sort(fruits);
        System.out.println("\nSau khi sắp xếp: " + fruits);
        
        // Đảo ngược
        Collections.reverse(fruits);
        System.out.println("Sau khi đảo: " + fruits);
        
        // Trộn ngẫu nhiên
        Collections.shuffle(fruits);
        System.out.println("Sau khi trộn: " + fruits);
        
        // Xóa tất cả
        fruits.clear();
        System.out.println("Sau khi clear: " + fruits);
        System.out.println("Rỗng? " + fruits.isEmpty());
    }
}
````

**Output:**
````
Danh sách: [Táo, Chuối, Cam, Dưa hấu]
Sau khi thêm: [Táo, Xoài, Chuối, Cam, Dưa hấu]
Phần tử đầu: Táo
Sau khi sửa: [Táo Đỏ, Xoài, Chuối, Cam, Dưa hấu]
Sau khi xóa: [Xoài, Cam, Dưa hấu]
Có Cam không? true
Số lượng: 3
````
### 4.2 LinkedList
LinkedList sử dụng cấu trúc danh sách liên kết đôi (doubly-linked list).
#### Đặc điểm:

 Chèn/xóa nhanh ở đầu và cuối: O(1)

 Chèn/xóa ở giữa tốt hơn ArrayList (không cần shift)

 Có thể dùng như Stack hoặc Queue

 Truy cập theo index chậm: O(n)

 Tốn bộ nhớ hơn (lưu con trỏ prev/next)

Khi nào dùng LinkedList:

Thêm/xóa ở đầu hoặc cuối nhiều

Không cần truy cập random

Cần implement Stack hoặc Queue

Chèn/xóa giữa list nhiều
```java
import java.util.*;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> animals = new LinkedList<>();
        
        // Thêm phần tử
        animals.add("Chó");
        animals.add("Mèo");
        animals.add("Gà");
        
        // LinkedList có thêm các method đặc biệt
        animals.addFirst("Voi");     // Thêm đầu
        animals.addLast("Ngựa");     // Thêm cuối
        System.out.println("Danh sách: " + animals);
        
        // Lấy phần tử (không xóa)
        String first = animals.getFirst();  // Lấy đầu
        String last = animals.getLast();    // Lấy cuối
        System.out.println("Đầu: " + first + ", Cuối: " + last);
        
        // Lấy và xóa
        animals.removeFirst();  // Xóa đầu
        animals.removeLast();   // Xóa cuối
        System.out.println("Sau khi xóa: " + animals);
        
        // Dùng như Stack (LIFO - Last In First Out)
        System.out.println("\n=== Dùng như Stack ===");
        animals.push("Tiger");  // Đẩy vào đầu
        System.out.println("Sau push: " + animals);
        String popped = animals.pop();  // Lấy ra từ đầu
        System.out.println("Popped: " + popped);
        
        // Dùng như Queue (FIFO - First In First Out)
        System.out.println("\n=== Dùng như Queue ===");
        animals.offer("Lion");   // Thêm vào cuối (như enqueue)
        System.out.println("Sau offer: " + animals);
        String polled = animals.poll();  // Lấy từ đầu (như dequeue)
        System.out.println("Polled: " + polled);
        
        System.out.println("Cuối cùng: " + animals);
    }
}
````
### 4.3 Vector và Stack

Vector: Giống ArrayList nhưng synchronized (thread-safe). Ít dùng hiện nay vì hiệu năng kém hơn.

Stack: Kế thừa Vector, cài đặt cấu trúc Stack (LIFO - Last In First Out).
```` java
import java.util.*;

public class StackDemo {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>();
        
        // Push - Đẩy vào stack
        stack.push("Đĩa 1");
        stack.push("Đĩa 2");
        stack.push("Đĩa 3");
        System.out.println("Stack: " + stack);  // [Đĩa 1, Đĩa 2, Đĩa 3]
        
        // Peek - Xem phần tử trên cùng (không xóa)
        String top = stack.peek();
        System.out.println("Trên cùng: " + top);  // Đĩa 3
        System.out.println("Stack vẫn: " + stack);
        
        // Pop - Lấy và xóa phần tử trên cùng
        String popped = stack.pop();
        System.out.println("Lấy ra: " + popped);  // Đĩa 3
        System.out.println("Stack còn: " + stack);  // [Đĩa 1, Đĩa 2]
        
        // Search - Tìm vị trí (1-based từ trên xuống)
        int position = stack.search("Đĩa 1");
        System.out.println("Vị trí Đĩa 1: " + position);  // 2 (từ trên xuống)
        
        // Empty - Kiểm tra rỗng
        System.out.println("Rỗng? " + stack.empty());  // false
        
        // Ứng dụng thực tế: Kiểm tra dấu ngoặc hợp lệ
        System.out.println("\n=== Kiểm tra dấu ngoặc ===");
        System.out.println("()[]{}     -> " + isValidParentheses("()[]{}"));     // true
        System.out.println("([{}])     -> " + isValidParentheses("([{}])"));     // true
        System.out.println("([)]       -> " + isValidParentheses("([)]"));       // false
        System.out.println("((())      -> " + isValidParentheses("((())"));      // false
        System.out.println("(          -> " + isValidParentheses("("));          // false
    }
    
    public static boolean isValidParentheses(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (char c : s.toCharArray()) {
            // Nếu là dấu mở, push vào stack
            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } 
            // Nếu là dấu đóng
            else {
                // Stack rỗng -> không có dấu mở tương ứng
                if (stack.isEmpty()) return false;
                
                char top = stack.pop();
                // Kiểm tra cặp
                if (c == ')' && top != '(') return false;
                if (c == ']' && top != '[') return false;
                if (c == '}' && top != '{') return false;
            }
        }
        
        // Stack phải rỗng (tất cả dấu mở đã được đóng)
        return stack.isEmpty();
    }
}
````
##  SET - Tập hợp không trùng lặp
Set không cho phép các phần tử trùng lặp, không có thứ tự index (không thể get theo vị trí).
### 5.1 HashSet
HashSet sử dụng hash table để lưu trữ, không đảm bảo thứ tự.
Đặc điểm:

 Thêm/xóa/tìm kiếm rất nhanh: O(1)

 Không cho phép trùng lặp

 Hiệu năng tốt nhất trong các Set

 Không có thứ tự

 Chỉ cho phép 1 phần tử null

Khi nào dùng HashSet:

Cần loại bỏ trùng lặp

Kiểm tra tồn tại nhanh

Không quan tâm thứ tự

Cần hiệu năng cao
```java
import java.util.*;

public class HashSetDemo {
    public static void main(String[] args) {
        Set<String> colors = new HashSet<>();
        
        // Thêm phần tử
        colors.add("Đỏ");
        colors.add("Xanh");
        colors.add("Vàng");
        colors.add("Đỏ");  // Trùng lặp - không được thêm
        System.out.println("Set: " + colors);
        System.out.println("Kích thước: " + colors.size());  // 3, không phải 4
        
        // Kiểm tra tồn tại
        boolean hasRed = colors.contains("Đỏ");
        System.out.println("Có màu Đỏ? " + hasRed);
        
        // Xóa phần tử
        colors.remove("Xanh");
        System.out.println("Sau khi xóa: " + colors);
        
        // Duyệt qua Set
        System.out.println("\n=== Duyệt Set ===");
        for (String color : colors) {
            System.out.println("- " + color);
        }
        
        // Ví dụ: Loại bỏ trùng lặp từ List
        System.out.println("\n=== Loại bỏ trùng lặp ===");
        List<Integer> numbers = Arrays.asList(1, 2, 3, 2, 4, 3, 5, 1, 6, 2);
        System.out.println("List gốc: " + numbers);
        
        Set<Integer> uniqueNumbers = new HashSet<>(numbers);
        System.out.println("Set (không trùng): " + uniqueNumbers);
        
        List<Integer> uniqueList = new ArrayList<>(uniqueNumbers);
        System.out.println("List mới: " + uniqueList);
        
        // Các phép toán tập hợp
        System.out.println("\n=== Phép toán tập hợp ===");
        Set<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));
        Set<Integer> set2 = new HashSet<>(Arrays.asList(4, 5, 6, 7, 8));
        
        // Hợp (Union)
        Set<Integer> union = new HashSet<>(set1);
        union.addAll(set2);
        System.out.println("Hợp: " + union);  // [1, 2, 3, 4, 5, 6, 7, 8]
        
        // Giao (Intersection)
        Set<Integer> intersection = new HashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Giao: " + intersection);  // [4, 5]
        
        // Hiệu (Difference)
        Set<Integer> difference = new HashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Hiệu: " + difference);  // [1, 2, 3]
    }
}
````
### 5.2 LinkedHashSet
LinkedHashSet giữ thứ tự insertion (thứ tự thêm vào).
Đặc điểm:

 Giữ thứ tự thêm vào

 Không trùng lặp như HashSet

Khi nào dùng LinkedHashSet:

Cần loại bỏ trùng lặp NHƯNG giữ thứ tự

Cần duyệt theo thứ tự thêm vào
```java
import java.util.*;

public class LinkedHashSetDemo {
    public static void main(String[] args) {
        System.out.println("=== HashSet - Không có thứ tự ===");
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Chuối");
        hashSet.add("Táo");
        hashSet.add("Cam");
        hashSet.add("Dưa");
        System.out.println(hashSet);  // Thứ tự ngẫu nhiên
        
        System.out.println("\n=== LinkedHashSet - Giữ thứ tự thêm vào ===");
        Set<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("Chuối");
        linkedHashSet.add("Táo");
        linkedHashSet.add("Cam");
        linkedHashSet.add("Dưa");
        System.out.println(linkedHashSet);  // Chuối, Táo, Cam, Dưa
        
        // Ứng dụng: Loại bỏ trùng lặp NHƯNG giữ thứ tự ban đầu
        System.out.println("\n=== Loại trùng giữ thứ tự ===");
        List<String> words = Arrays.asList("apple", "banana", "apple", "cherry", "banana", "date");
        System.out.println("List gốc: " + words);
        
        Set<String> uniqueWords = new LinkedHashSet<>(words);
        System.out.println("Không trùng, giữ thứ tự: " + uniqueWords);
    }
}
````
### 5.3 TreeSet
TreeSet lưu trữ các phần tử theo thứ tự sắp xếp tự động (sorted order).
#### Đặc điểm:
Ưu điểm:

 Tự động sắp xếp

 Không trùng lặp

 Có các method đặc biệt: first(), last(), floor(), ceiling()

Nhược điểm:

 Chậm hơn HashSet: O(log n)

 Không cho phép null

 Phần tử phải implement Comparable hoặc cần Comparator

Khi nào dùng TreeSet:

Cần dữ liệu luôn được sắp xếp

Cần tìm phần tử gần nhất (floor/ceiling)

Không cần hiệu năng cao nhất
```` java
import java.util.*;

public class TreeSetDemo {
    public static void main(String[] args) {
        Set<Integer> numbers = new TreeSet<>();
        
        // Thêm các số không theo thứ tự
        numbers.add(5);
        numbers.add(2);
        numbers.add(8);
        numbers.add(1);
        numbers.add(9);
        numbers.add(3);
        
        // TreeSet tự động sắp xếp
        System.out.println("TreeSet: " + numbers);  // [1, 2, 3, 5, 8, 9]
        
        // TreeSet với String - Sắp xếp theo alphabet
        Set<String> names = new TreeSet<>();
        names.add("Dũng");
        names.add("An");
        names.add("Chính");
        names.add("Bình");
        System.out.println("Names: " + names);  // [An, Bình, Chính, Dũng]
        
        // TreeSet với Comparator tùy chỉnh - Sắp xếp ngược
        Set<String> reversedNames = new TreeSet<>(Collections.reverseOrder());
        reversedNames.add("Dũng");
        reversedNames.add("An");
        reversedNames.add("Chính");
        reversedNames.add("Bình");
        System.out.println("Reversed: " + reversedNames);  // [Dũng, Chính, Bình, An]
        
        // TreeSet với Object tùy chỉnh
        Set<Person> people = new TreeSet<>(Comparator.comparing(Person::getAge));
        people.add(new Person("An", 25));
        people.add(new Person("Bình", 20));
        people.add(new Person("Chính", 30));
        people.add(new Person("Dũng", 22));
        
        System.out.println("\n=== Danh sách người (sắp xếp theo tuổi) ===");
        for (Person p : people) {
            System.out.println(p);
        }
        
        // Các method đặc biệt của TreeSet
        TreeSet<Integer> treeSet = new TreeSet<>(Arrays.asList(1, 5, 10, 15, 20, 25));
        
        System.out.println("\n=== Method đặc biệt của TreeSet ===");
        System.out.println("First (nhỏ nhất): " + treeSet.first());  // 1
        System.out.println("Last (lớn nhất): " + treeSet.last());    // 25
        
        // floor: Phần tử lớn nhất <= giá trị cho trước
        System.out.println("Floor(12): " + treeSet.floor(12));  // 10
        
        // ceiling: Phần tử nhỏ nhất >= giá trị cho trước
        System.out.println("Ceiling(12): " + treeSet.ceiling(12));  // 15
        
        // higher: Phần tử nhỏ nhất > giá trị cho trước
        System.out.println("Higher(15): " + treeSet.higher(15));  // 20
        
        // lower: Phần tử lớn nhất < giá trị cho trước
        System.out.println("Lower(15): " + treeSet.lower(15));  // 10
        
        // SubSet
        System.out.println("SubSet [10, 20): " + treeSet.subSet(10, 20));  // [10, 15]
        System.out.println("HeadSet < 15: " + treeSet.headSet(15));  // [1, 5, 10]
        System.out.println("TailSet >= 15: " + treeSet.tailSet(15));  // [15, 20, 25]
    }
}

class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() { return name; }
    public int getAge() { return age; }
    
    @Override
    public String toString() {
        return name + " (" + age + " tuổi)";
    }
}
public class SetComparison {
    public static void main(String[] args) {
        System.out.println("=== HashSet - Không có thứ tự ===");
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Zebra");
        hashSet.add("Apple");
        hashSet.add("Mango");
        hashSet.add("Banana");
        System.out.println(hashSet);  // Thứ tự ngẫu nhiên
        
        System.out.println("\n=== LinkedHashSet - Giữ thứ tự thêm vào ===");
        Set<String> linkedHashSet = new LinkedHashSet<>();
        linkedHashSet.add("Zebra");
        linkedHashSet.add("Apple");
        linkedHashSet.add("Mango");
        linkedHashSet.add("Banana");
        System.out.println(linkedHashSet);  // Zebra, Apple, Mango, Banana
        
        System.out.println("\n=== TreeSet - Sắp xếp tự động ===");
        Set<String> treeSet = new TreeSet<>();
        treeSet.add("Zebra");
        treeSet.add("Apple");
        treeSet.add("Mango");
        treeSet.add("Banana");
        System.out.println(treeSet);  // Apple, Banana, Mango, Zebra
    }
}
````
##  QUEUE - Hàng đợi
Queue là collection theo nguyên tắc FIFO (First In First Out) - vào trước ra trước.
### 6.1 PriorityQueue
PriorityQueue sắp xếp các phần tử theo độ ưu tiên (priority).

### Khi nào dùng PriorityQueue:

Task scheduling theo priority

Tìm k phần tử nhỏ/lớn nhất

Dijkstra algorithm

Event-driven simulation
```` java
import java.util.*;

public class PriorityQueueDemo {
    public static void main(String[] args) {
        // PriorityQueue với số - Tự động sắp xếp tăng dần (min heap)
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        pq.offer(5);  // offer = add
        pq.offer(2);
        pq.offer(8);
        pq.offer(1);
        pq.offer(9);
        
        System.out.println("PriorityQueue: " + pq);
        
        // Poll - Lấy và xóa phần tử nhỏ nhất
        System.out.println("\n=== Poll theo thứ tự priority ===");
        while (!pq.isEmpty()) {
            System.out.println("Poll: " + pq.poll());
        }
        // Output: 1, 2, 5, 8, 9
        
        // PriorityQueue với Comparator (max heap - lớn nhất trước)
        System.out.println("\n=== Max Heap ===");
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        maxHeap.offer(5);
        maxHeap.offer(2);
        maxHeap.offer(8);
        maxHeap.offer(1);
        maxHeap.offer(9);
        
        while (!maxHeap.isEmpty()) {
            System.out.println("Poll: " + maxHeap.poll());
        }
        // Output: 9, 8, 5, 2, 1
        
        // Ví dụ thực tế: Hệ thống ưu tiên Task
        System.out.println("\n=== Task Priority System ===");
        PriorityQueue<Task> tasks = new PriorityQueue<>(
            Comparator.comparing(Task::getPriority).reversed()
        );
        
        tasks.offer(new Task("Bug fix", 5));
        tasks.offer(new Task("Feature A", 3));
        tasks.offer(new Task("Critical bug", 10));
        tasks.offer(new Task("Documentation", 1));
        tasks.offer(new Task("Refactoring", 4));
        
        System.out.println("Thứ tự xử lý:");
        while (!tasks.isEmpty()) {
            Task task = tasks.poll();
            System.out.println(task);
        }
        
        // Ứng dụng: Tìm k phần tử lớn nhất
        System.out.println("\n=== Tìm 3 số lớn nhất ===");
        int[] nums = {3, 1, 5, 12, 2, 11, 8, 7};
        int k = 3;
        
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int num : nums) {
            minHeap.offer(num);
            if (minHeap.size() > k) {
                minHeap.poll();  // Xóa số nhỏ nhất
            }
        }
        
        System.out.println("3 số lớn nhất: " + minHeap);
    }
}

class Task {
    private String name;
    private int priority;
    
    public Task(String name, int priority) {
        this.name = name;
        this.priority = priority;
    }
    
    public int getPriority() { return priority; }
    
    @Override
    public String toString() {
        return name + " (priority: " + priority + ")";
    }
}
````
## 6.2 ArrayDeque
ArrayDeque (Double-Ended Queue) cho phép thêm/xóa từ cả hai đầu.

### Khi nào dùng ArrayDeque:

Cần Stack (thay vì dùng Stack class)
Cần Queue hiệu năng cao
Thao tác hai đầu nhiều
```java
import java.util.*;

public class ArrayDequeDemo {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        
        // Thêm vào đầu
        deque.addFirst("A");
        deque.addFirst("B");
        System.out.println("Sau addFirst: " + deque);  // [B, A]
        
        // Thêm vào cuối
        deque.addLast("C");
        deque.addLast("D");
        System.out.println("Sau addLast: " + deque);   // [B, A, C, D]
        
        // Lấy từ đầu (không xóa)
        System.out.println("peekFirst: " + deque.peekFirst());  // B
        
        // Lấy từ cuối (không xóa)
        System.out.println("peekLast: " + deque.peekLast());    // D
        
        // Lấy và xóa từ đầu
        String first = deque.removeFirst();
        System.out.println("removeFirst: " + first + ", Deque: " + deque);
        
        // Lấy và xóa từ cuối
        String last = deque.removeLast();
        System.out.println("removeLast: " + last + ", Deque: " + deque);
        
        // Dùng như Stack (LIFO)
        System.out.println("\n=== Dùng như Stack (LIFO) ===");
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(1);
        stack.push(2);
        stack.push(3);
        System.out.println("Stack: " + stack);  // [3, 2, 1]
        System.out.println("Pop: " + stack.pop());  // 3
        System.out.println("Peek: " + stack.peek());  // 2
        
        // Dùng như Queue (FIFO)
        System.out.println("\n=== Dùng như Queue (FIFO) ===");
        Deque<Integer> queue = new ArrayDeque<>();
        queue.offer(1);  // Thêm vào cuối
        queue.offer(2);
        queue.offer(3);
        System.out.println("Queue: " + queue);  // [1, 2, 3]
        System.out.println("Poll: " + queue.poll());  // 1 (lấy từ đầu)
        System.out.println("Peek: " + queue.peek());  // 2
    }
}
````
Lưu ý: ArrayDeque là lựa chọn tốt nhất cho Stack và Queue 
trong Java hiện đại, thay thế cho Stack class và LinkedList.

## MAP - Ánh xạ Key-Value
Map lưu trữ dữ liệu dưới dạng cặp key-value. Mỗi key là duy nhất, value có thể trùng lặp.
### 7.1 HashMap
HashMap là implementation phổ biến nhất của Map, sử dụng hash table.

### Khi nào dùng HashMap:

Cần tra cứu nhanh theo key
Không quan tâm thứ tự
Không cần thread-safe
Lưu cache, dictionary, counter

<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;">HashMap <strong>không đảm bảo thứ tự</strong> các phần tử! Nếu cần giữ thứ tự insertion, dùng <code>LinkedHashMap</code>. Nếu cần keys được sắp xếp tự động, dùng <code>TreeMap</code>.</p>
</div>


---

```java
import java.util.*;

public class HashMapDemo {
    public static void main(String[] args) {
        // Tạo HashMap
        Map<String, Integer> ages = new HashMap<>();
        
        // Thêm cặp key-value
        ages.put("An", 25);
        ages.put("Bình", 30);
        ages.put("Chính", 28);
        ages.put("Dũng", 22);
        System.out.println("Map: " + ages);
        
        // Lấy giá trị theo key
        int ageOfAn = ages.get("An");
        System.out.println("Tuổi của An: " + ageOfAn);
        
        // Kiểm tra key tồn tại
        boolean hasChinh = ages.containsKey("Chính");
        System.out.println("Có Chính không? " + hasChinh);
        
        // Kiểm tra value tồn tại
        boolean hasAge30 = ages.containsValue(30);
        System.out.println("Có ai 30 tuổi? " + hasAge30);
        
        // Cập nhật giá trị
        ages.put("An", 26);  // Ghi đè giá trị cũ
        System.out.println("Sau khi cập nhật: " + ages);
        
        // getOrDefault - Trả về giá trị mặc định nếu key không tồn tại
        int ageOfE = ages.getOrDefault("E", 0);
        System.out.println("Tuổi của E: " + ageOfE);
        
        // putIfAbsent - Chỉ thêm nếu key chưa tồn tại
        ages.putIfAbsent("An", 100);  // Không thay đổi vì đã có
        ages.putIfAbsent("E", 35);    // Thêm mới
        System.out.println("Sau putIfAbsent: " + ages);
        
        // Xóa
        ages.remove("Dũng");
        System.out.println("Sau khi xóa: " + ages);
        
        // Kích thước
        System.out.println("Số lượng: " + ages.size());
        
        System.out.println("\n=== Duyệt qua Map ===");
        
        // Cách 1: Duyệt qua keySet
        System.out.println("1. KeySet:");
        for (String name : ages.keySet()) {
            System.out.println(name + ": " + ages.get(name));
        }
        
        // Cách 2: Duyệt qua values
        System.out.println("\n2. Values:");
        for (Integer age : ages.values()) {
            System.out.println(age);
        }
        
        // Cách 3: Duyệt qua entrySet (TỐT NHẤT - chỉ duyệt 1 lần)
        System.out.println("\n3. EntrySet (Khuyên dùng):");
        for (Map.Entry<String, Integer> entry : ages.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
        
        // Cách 4: forEach với Lambda (Java 8+)
        System.out.println("\n4. forEach Lambda:");
        ages.forEach((name, age) -> 
            System.out.println(name + " là " + age + " tuổi")
        );
        
        // Ứng dụng: Đếm tần suất
        System.out.println("\n=== Đếm tần suất từ ===");
        String text = "apple banana apple cherry banana apple date";
        Map<String, Integer> frequency = new HashMap<>();
        
        for (String word : text.split(" ")) {
            frequency.put(word, frequency.getOrDefault(word, 0) + 1);
        }
        
        System.out.println("Tần suất: " + frequency);
        
        // Tìm từ xuất hiện nhiều nhất
        String mostFrequent = Collections.max(frequency.entrySet(), 
            Map.Entry.comparingByValue()).getKey();
        System.out.println("Từ xuất hiện nhiều nhất: " + mostFrequent);
    }
}
````
### 7.2 LinkedHashMap
LinkedHashMap giữ thứ tự insertion hoặc access order.
#### Đặc điểm:

 Giữ thứ tự thêm vào
 Có thể giữ thứ tự truy cập (access order)

#### Khi nào dùng LinkedHashMap:

Cần giữ thứ tự insertion
Implement LRU Cache
Cần duyệt theo thứ tự đã thêm
```java
import java.util.*;

public class LinkedHashMapDemo {
    public static void main(String[] args) {
        // HashMap - Không có thứ tự
        System.out.println("=== HashMap - Không thứ tự ===");
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Zebra", 1);
        hashMap.put("Apple", 2);
        hashMap.put("Mango", 3);
        hashMap.put("Banana", 4);
        System.out.println(hashMap);  // Thứ tự ngẫu nhiên
        
        // LinkedHashMap - Giữ thứ tự thêm vào
        System.out.println("\n=== LinkedHashMap - Giữ thứ tự ===");
        Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("Zebra", 1);
        linkedHashMap.put("Apple", 2);
        linkedHashMap.put("Mango", 3);
        linkedHashMap.put("Banana", 4);
        System.out.println(linkedHashMap);  // Zebra, Apple, Mango, Banana
        
        // LinkedHashMap với access order (LRU Cache)
        System.out.println("\n=== LRU Cache ===");
        Map<String, Integer> lruCache = new LinkedHashMap<>(16, 0.75f, true) {
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > 3;  // Giữ tối đa 3 phần tử
            }
        };
        
        lruCache.put("A", 1);
        lruCache.put("B", 2);
        lruCache.put("C", 3);
        System.out.println("Ban đầu: " + lruCache);
        
        lruCache.get("A");  // Truy cập A
        System.out.println("Sau get(A): " + lruCache);
        
        lruCache.put("D", 4);  // B sẽ bị xóa (ít dùng nhất)
        System.out.println("Sau put(D): " + lruCache);
    }
}
````
### 7.3 TreeMap
TreeMap lưu trữ các entry theo thứ tự sắp xếp của key.
#### Đặc điểm:

 Tự động sắp xếp theo key
 Có các method đặc biệt: firstKey(), lastKey(), floorKey()


#### Khi nào dùng TreeMap:

Cần dữ liệu luôn sắp xếp theo key
Cần range query (subMap, headMap, tailMap)
Cần tìm key gần nhất
```java
import java.util.*;

public class TreeMapDemo {
    public static void main(String[] args) {
        // TreeMap tự động sắp xếp theo key
        Map<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("Dog", 3);
        treeMap.put("Apple", 1);
        treeMap.put("Cat", 2);
        treeMap.put("Banana", 4);
        
        System.out.println("TreeMap (sắp xếp): " + treeMap);
        // {Apple=1, Banana=4, Cat=2, Dog=3}
        
        // TreeMap với số
        TreeMap<Integer, String> scores = new TreeMap<>();
        scores.put(85, "An");
        scores.put(92, "Bình");
        scores.put(78, "Chính");
        scores.put(95, "Dũng");
        scores.put(88, "Hoa");
        
        System.out.println("\n=== Điểm số sắp xếp ===");
        System.out.println(scores);
        
        // Các method đặc biệt
        System.out.println("\n=== Method đặc biệt ===");
        System.out.println("First key: " + scores.firstKey());  // 78
        System.out.println("Last key: " + scores.lastKey());    // 95
        System.out.println("First entry: " + scores.firstEntry());
        System.out.println("Last entry: " + scores.lastEntry());
        
        // floorKey: Key lớn nhất <= giá trị cho trước
        System.out.println("floorKey(90): " + scores.floorKey(90));  // 88
        
        // ceilingKey: Key nhỏ nhất >= giá trị cho trước
        System.out.println("ceilingKey(90): " + scores.ceilingKey(90));  // 92
        
        // higherKey: Key nhỏ nhất > giá trị cho trước
        System.out.println("higherKey(88): " + scores.higherKey(88));  // 92
        
        // lowerKey: Key lớn nhất < giá trị cho trước
        System.out.println("lowerKey(88): " + scores.lowerKey(88));  // 85
        
        // SubMap - Lấy một phần map
        System.out.println("\n=== SubMap ===");
        System.out.println("SubMap [80, 90): " + scores.subMap(80, 90));
        System.out.println("HeadMap < 88: " + scores.headMap(88));
        System.out.println("TailMap >= 88: " + scores.tailMap(88));
        
        // Sắp xếp ngược
        System.out.println("\n=== Sắp xếp ngược ===");
        TreeMap<Integer, String> descScores = new TreeMap<>(Collections.reverseOrder());
        descScores.putAll(scores);
        System.out.println(descScores);
    }
}
````
### Ví dụ thực tế
#### Ví dụ 1: Quản lý sinh viên
```` java
import java.util.*;

class Student {
    private String id;
    private String name;
    private double gpa;
    
    public Student(String id, String name, double gpa) {
        this.id = id;
        this.name = name;
        this.gpa = gpa;
    }
    
    public String getId() { return id; }
    public String getName() { return name; }
    public double getGpa() { return gpa; }
    
    @Override
    public String toString() {
        return String.format("%s - %s (GPA: %.2f)", id, name, gpa);
    }
}

public class StudentManagement {
    public static void main(String[] args) {
        // List để lưu danh sách sinh viên
        List<Student> students = new ArrayList<>();
        students.add(new Student("SV001", "Nguyễn Văn An", 3.5));
        students.add(new Student("SV002", "Trần Thị Bình", 3.8));
        students.add(new Student("SV003", "Lê Văn Chính", 3.2));
        students.add(new Student("SV004", "Phạm Thị Dung", 3.9));
        
        System.out.println("=== DANH SÁCH SINH VIÊN ===");
        students.forEach(System.out::println);
        
        // Map để tra cứu nhanh theo ID
        Map<String, Student> studentMap = new HashMap<>();
        for (Student s : students) {
            studentMap.put(s.getId(), s);
        }
        
        System.out.println("\n=== TRA CỨU SINH VIÊN ===");
        Student found = studentMap.get("SV002");
        System.out.println("Tìm SV002: " + found);
        
        // Sắp xếp theo GPA
        System.out.println("\n=== SẮP XẾP THEO GPA (GIẢM DẦN) ===");
        Collections.sort(students, Comparator.comparing(Student::getGpa).reversed());
        students.forEach(System.out::println);
        
        // Tìm sinh viên GPA cao nhất
        Student topStudent = Collections.max(students, Comparator.comparing(Student::getGpa));
        System.out.println("\nSinh viên xuất sắc nhất: " + topStudent);
        
        // Lọc sinh viên GPA >= 3.5
        System.out.println("\n=== SINH VIÊN GPA >= 3.5 ===");
        students.stream()
            .filter(s -> s.getGpa() >= 3.5)
            .forEach(System.out::println);
    }
}
````

**Kết quả:**
```
=== DANH SÁCH SINH VIÊN ===
SV001 - Nguyễn Văn An (GPA: 3.50)
SV002 - Trần Thị Bình (GPA: 3.80)
SV003 - Lê Văn Chính (GPA: 3.20)
SV004 - Phạm Thị Dung (GPA: 3.90)

=== TRA CỨU SINH VIÊN ===
Tìm SV002: SV002 - Trần Thị Bình (GPA: 3.80)

=== SẮP XẾP THEO GPA (GIẢM DẦN) ===
SV004 - Phạm Thị Dung (GPA: 3.90)
SV002 - Trần Thị Bình (GPA: 3.80)
SV001 - Nguyễn Văn An (GPA: 3.50)
SV003 - Lê Văn Chính (GPA: 3.20)

Sinh viên xuất sắc nhất: SV004 - Phạm Thị Dung (GPA: 3.90)

=== SINH VIÊN GPA >= 3.5 ===
SV004 - Phạm Thị Dung (GPA: 3.90)
SV002 - Trần Thị Bình (GPA: 3.80)
SV001 - Nguyễn Văn An (GPA: 3.50)
````
### Ví dụ 2: Giỏ hàng mua sắm
```` java
import java.util.*;

class Product {
    private String id;
    private String name;
    private double price;
    
    public Product(String id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }
    
    public String getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
}

class ShoppingCart {
    private Map<String, Integer> items = new HashMap<>();
    private Map<String, Product> products = new HashMap<>();
    
    public void addProduct(Product product, int quantity) {
        products.put(product.getId(), product);
        items.put(product.getId(), items.getOrDefault(product.getId(), 0) + quantity);
        System.out.println("Đã thêm: " + product.getName() + " x" + quantity);
    }
    
    public void removeProduct(String productId) {
        if (items.containsKey(productId)) {
            items.remove(productId);
            System.out.println("Đã xóa sản phẩm: " + productId);
        }
    }
    
    public void display() {
        if (items.isEmpty()) {
            System.out.println("Giỏ hàng trống!");
            return;
        }
        
        System.out.println("\n=== GIỎ HÀNG ===");
        double total = 0;
        for (Map.Entry<String, Integer> entry : items.entrySet()) {
            String id = entry.getKey();
            int quantity = entry.getValue();
            Product product = products.get(id);
            double subtotal = product.getPrice() * quantity;
            total += subtotal;
            
            System.out.printf("%s x%d = %.0fđ\n", 
                product.getName(), quantity, subtotal);
        }
        System.out.printf("TỔNG CỘNG: %.0fđ\n", total);
    }
}

public class ShoppingCartDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        cart.addProduct(new Product("P001", "Laptop", 15000000), 1);
        cart.addProduct(new Product("P002", "Mouse", 200000), 2);
        cart.addProduct(new Product("P003", "Keyboard", 500000), 1);
        
        cart.display();
        
        System.out.println("\n=== THÊM MOUSE ===");
        cart.addProduct(new Product("P002", "Mouse", 200000), 1);
        cart.display();
        
        System.out.println("\n=== XÓA KEYBOARD ===");
        cart.removeProduct("P003");
        cart.display();
    }
}
````

**Kết quả:**
```
Đã thêm: Laptop x1
Đã thêm: Mouse x2
Đã thêm: Keyboard x1

=== GIỎ HÀNG ===
Laptop x1 = 15000000đ
Mouse x2 = 400000đ
Keyboard x1 = 500000đ
TỔNG CỘNG: 15900000đ

=== THÊM MOUSE ===
Đã thêm: Mouse x1

=== GIỎ HÀNG ===
Laptop x1 = 15000000đ
Mouse x3 = 600000đ
Keyboard x1 = 500000đ
TỔNG CỘNG: 16100000đ

=== XÓA KEYBOARD ===
Đã xóa sản phẩm: P003

=== GIỎ HÀNG ===
Laptop x1 = 15000000đ
Mouse x3 = 600000đ
TỔNG CỘNG: 15600000đ
````
## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** ArrayList và LinkedList khác nhau về performance như thế nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; text-align: left; border: 1px solid #dee2e6;">Operation</th>
        <th style="padding: 10px; text-align: left; border: 1px solid #dee2e6;">ArrayList</th>
        <th style="padding: 10px; text-align: left; border: 1px solid #dee2e6;">LinkedList</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Random Access</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅ O(1)</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌ O(n)</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Insert/Delete đầu/cuối</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌ O(n)</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅ O(1)</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Insert/Delete giữa</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌ O(n)</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅ O(1)*</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Memory</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">✅ Compact</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">❌ More overhead</td>
      </tr>
    </table>
    <p style="margin: 10px 0 0 0; font-size: 14px; color: #666;">* Nếu đã có reference đến node</p>
  </div>
</details>

**Câu 2:** Khi nào nên dùng HashMap vs TreeMap vs LinkedHashMap?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🗺️ HashMap:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Không cần order</li>
      <li>✅ Performance cao nhất (O(1))</li>
      <li>✅ Cho phép 1 null key</li>
      <li>❌ Không đảm bảo thứ tự</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🔗 LinkedHashMap:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Giữ thứ tự insertion</li>
      <li>✅ Performance tốt (O(1))</li>
      <li>✅ Cho phép 1 null key</li>
      <li>❌ Memory overhead cao hơn</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🌳 TreeMap:</strong></p>
    <ul style="margin: 0;">
      <li>✅ Keys được sorted tự động</li>
      <li>✅ Implements NavigableMap</li>
      <li>❌ Chậm hơn (O(log n))</li>
      <li>❌ Không cho phép null key</li>
    </ul>
  </div>
</details>

**Câu 3:** HashSet vs TreeSet vs LinkedHashSet - Dùng khi nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0;"><strong>HashSet:</strong> Fast (O(1)), không order, cho phép null → Dùng khi cần uniqueness và performance</p>
    <p style="margin: 10px 0 0 0;"><strong>TreeSet:</strong> Sorted (O(log n)), không null → Dùng khi cần sorted data</p>
    <p style="margin: 10px 0 0 0;"><strong>LinkedHashSet:</strong> Insertion order (O(1)), cho phép null → Dùng khi cần uniqueness + order</p>
  </div>
</details>

**Câu 4:** Tại sao phải override equals() và hashCode() cùng nhau?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 15px 0;"><strong>✅ BẮT BUỘC phải override cả 2!</strong></p>
    <p style="margin: 0 0 10px 0;"><strong>Contract:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Nếu <code>a.equals(b) == true</code> → <code>a.hashCode() == b.hashCode()</code></li>
      <li>Nếu <code>a.hashCode() == b.hashCode()</code> → <code>a.equals(b)</code> CÓ THỂ true hoặc false</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>Nếu không override cả 2:</strong></p>
    <ul style="margin: 0;">
      <li>❌ HashMap/HashSet hoạt động sai</li>
      <li>❌ Không tìm được object đã lưu</li>
      <li>❌ Duplicate objects trong Set</li>
    </ul>
  </div>
</details>

**Câu 5:** List vs Set vs Map - Khi nào dùng cái nào?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>📋 List (ArrayList, LinkedList):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Cho phép duplicates</li>
      <li>✅ Có thứ tự (index-based)</li>
      <li>✅ Access by index: <code>list.get(0)</code></li>
      <li>📌 Dùng khi: cần order, duplicates, access by index</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🎯 Set (HashSet, TreeSet):</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>✅ Không cho phép duplicates</li>
      <li>❌ Không có index</li>
      <li>✅ Fast lookup: <code>contains()</code></li>
      <li>📌 Dùng khi: cần uniqueness, remove duplicates</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🗺️ Map (HashMap, TreeMap):</strong></p>
    <ul style="margin: 0;">
      <li>✅ Key-value pairs</li>
      <li>✅ Keys unique, values có thể duplicate</li>
      <li>✅ Fast lookup by key: <code>get(key)</code></li>
      <li>📌 Dùng khi: cần mapping, lookup by key</li>
    </ul>
  </div>
</details>

</div>

### Kết luận
“Collections Framework không chỉ giúp lập trình viên xử lý dữ liệu hiệu quả mà còn là nền tảng cho các framework lớn như Spring, Hibernate... Việc nắm vững nó giúp bạn làm chủ ngôn ngữ Java trong mọi dự án thực tế.”
### Tài liệu tham khảo

Oracle Java Documentation - Collections

Java Collections API

Baeldung - Java Collections
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai3" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🏛️</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">OOP Principles trong Java</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">4 nguyên lý cốt lõi của lập trình hướng đối tượng: Encapsulation, Inheritance, Polymorphism, Abstraction</p>
    <div style="margin-top: 15px; display: flex; gap: 8px; flex-wrap: wrap;">
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">Java</span>
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">OOP</span>
    </div>
  </div>
</a>

<a href="/posts/bai6" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🟨</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">JavaScript cơ bản</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.95); font-size: 14px; line-height: 1.6;">Kiến thức nền tảng về JavaScript: Data types, OOP và Functional Programming</p>
    <div style="margin-top: 15px; display: flex; gap: 8px; flex-wrap: wrap;">
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">JavaScript</span>
      <span style="background: rgba(255,255,255,0.3); padding: 4px 10px; border-radius: 12px; font-size: 12px; color: white;">ES6</span>
    </div>
  </div>
</a>

<a href="/posts" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">📚</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Xem tất cả bài viết</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">Khám phá thêm nhiều bài viết về Java, JavaScript và Web Development</p>
  </div>
</a>

</div>


---