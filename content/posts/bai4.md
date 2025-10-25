---
title: "Exception Handling trong Java"
date: 2025-10-10T03:00:00Z

draft: false
---
<div style="background: #f8f9fa; border: 2px solid #e9ecef; border-radius: 8px; padding: 20px 30px; margin: 30px 0;">
  <h2 style="margin-top: 0; color: #2c3e50; font-size: 24px; border-bottom: 2px solid #4CAF50; padding-bottom: 10px;">📋 Mục lục</h2>
  <ol style="line-height: 2;">
    <li><a href="#giới-thiệu">Giới thiệu</a></li>
    <li><a href="#phân-loại-exception">Phân loại Exception</a></li>
    <li><a href="#cú-pháp-try-catch-finally">Cú pháp Try-Catch-Finally</a></li>
    <li><a href="#throw-và-throws">Throw và Throws</a></li>
    <li><a href="#custom-exception---tạo-exception-riêng">Custom Exception - Tạo Exception riêng</a></li>
    <li><a href="#best-practices---cách-viết-tốt">Best Practices - Cách viết tốt</a></li>
    <li><a href="#các-exception-phổ-biến">Các Exception phổ biến</a></li>
    <li><a href="#ví-dụ-thực-tế">Ví dụ thực tế</a></li>
    <li><a href="#bài-tập-thực-hành">Bài tập thực hành</a></li>
    <li><a href="#so-sánh-có-và-không-có-exception-handling">So sánh: Có và không có Exception Handling</a></li>
    <li><a href="#common-mistakes-lỗi-thường-gặp">Common Mistakes (Lỗi thường gặp)</a></li>
    <li><a href="#tips-nâng-cao">Tips nâng cao</a></li>
    <li><a href="#kết-luận">Kết luận</a></li>
    <li><a href="#tài-liệu-tham-khảo">Tài liệu tham khảo</a></li>
  </ol>
</div>

## Giới thiệu
Exception (ngoại lệ) là những sự kiện bất thường xảy ra trong quá trình chạy chương trình, làm gián đoạn luồng thực thi bình thường. Exception handling (xử lý ngoại lệ) là cơ chế giúp chương trình xử lý các lỗi một cách an toàn, tránh crash và cung cấp thông báo lỗi hữu ích cho người dùng.

Thay vì để chương trình bị dừng đột ngột khi gặp lỗi, Java cung cấp một cơ chế mạnh mẽ để "bắt" và xử lý các lỗi này một cách có kiểm soát.

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; margin: 25px 0; border-radius: 12px; color: white; box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">💡</span>
    <strong style="font-size: 18px;">Pro Tip</strong>
  </div>
  <p style="margin: 0; line-height: 1.6;">Exception handling không chỉ là "bắt lỗi" mà còn giúp chương trình <strong>gracefully recover</strong> từ lỗi. Thay vì crash, app có thể log error, thông báo user, và tiếp tục chạy. Đây là dấu hiệu của <strong>production-ready code</strong>!</p>
</div>

### Tại sao cần Exception Handling?
#### Ví dụ không có Exception Handling:
````java
public class NoExceptionHandling {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        System.out.println("Bắt đầu chương trình");
        
        // Lỗi: truy cập index không tồn tại
        System.out.println(numbers[10]);  // Crash tại đây!
        
        System.out.println("Kết thúc chương trình");  // Không bao giờ chạy đến đây
    }
}
````

**Output:**
````
Bắt đầu chương trình
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 5
````
Chương trình bị dừng đột ngột và dòng "Kết thúc chương trình" không bao giờ được in ra.
### Với Exception Handling:
````java
public class WithExceptionHandling {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        System.out.println("Bắt đầu chương trình");
        
        try {
            System.out.println(numbers[10]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Lỗi: Truy cập index không hợp lệ!");
            System.out.println("Chi tiết: " + e.getMessage());
        }
        
        System.out.println("Kết thúc chương trình");  // Vẫn chạy bình thường
    }
}
````

**Output:**
````
Bắt đầu chương trình
Lỗi: Truy cập index không hợp lệ!
Chi tiết: Index 10 out of bounds for length 5
Kết thúc chương trình
````
## Phân loại Exception
### 1. Checked Exception (Exception được kiểm tra)
Là các exception phải được xử lý tại compile-time. Nếu không xử lý, code sẽ không compile được.
Ví dụ:

#### IOException - Lỗi đọc/ghi file
#### SQLException - Lỗi database
#### ClassNotFoundException - Không tìm thấy class
#### FileNotFoundException - Không tìm thấy file
````java
import java.io.*;

public class CheckedExceptionDemo {
    public static void main(String[] args) {
        // ❌ Code này sẽ không compile nếu không có try-catch
        // FileReader reader = new FileReader("data.txt");
        
        // ✅ Phải bắt exception hoặc throws
        try {
            FileReader reader = new FileReader("data.txt");
            System.out.println("File được mở thành công");
            reader.close();
        } catch (FileNotFoundException e) {
            System.out.println("Không tìm thấy file: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Lỗi I/O: " + e.getMessage());
        }
    }
}
````
### 2. Unchecked Exception (Runtime Exception)
Là các exception không bắt buộc phải xử lý. Chúng xảy ra trong runtime và thường do lỗi logic.
### Ví dụ:

NullPointerException - Truy cập object null

ArrayIndexOutOfBoundsException - Index mảng vượt quá

ArithmeticException - Lỗi toán học (chia cho 0)

NumberFormatException - Parse số không hợp lệ

IllegalArgumentException - Tham số không hợp lệ
````java
public class UncheckedExceptionDemo {
    public static void main(String[] args) {
        // 1. NullPointerException
        String text = null;
        try {
            System.out.println(text.length());  // Lỗi!
        } catch (NullPointerException e) {
            System.out.println("Lỗi: Biến là null!");
        }
        
        // 2. ArithmeticException
        try {
            int result = 10 / 0;  // Chia cho 0
        } catch (ArithmeticException e) {
            System.out.println("Lỗi: Không thể chia cho 0!");
        }
        
        // 3. NumberFormatException
        try {
            int number = Integer.parseInt("abc");  // Không phải số
        } catch (NumberFormatException e) {
            System.out.println("Lỗi: Chuỗi không phải là số!");
        }
        
        // 4. ArrayIndexOutOfBoundsException
        int[] arr = {1, 2, 3};
        try {
            System.out.println(arr[10]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Lỗi: Index vượt quá kích thước mảng!");
        }
    }
}
````
### 3 Error
Error là các lỗi nghiêm trọng mà chương trình không nên xử lý, thường liên quan đến hệ thống.
Ví dụ:

- OutOfMemoryError - Hết bộ nhớ
- StackOverflowError - Stack bị tràn
- VirtualMachineError - Lỗi JVM
````java
public class ErrorDemo {
    // Ví dụ StackOverflowError
    public static void recursiveMethod() {
        recursiveMethod();  // Đệ quy vô hạn
    }
    
    public static void main(String[] args) {
        try {
            recursiveMethod();
        } catch (StackOverflowError e) {
            System.out.println("Lỗi: Stack overflow!");
        }
    }
}
````
## Cú pháp Try-Catch-Finally
### 1. Try-Catch cơ bản
````java
try {
    // Code có thể gây ra exception
} catch (ExceptionType e) {
    // Xử lý exception
}
### Ví dụ:
````java
public class TryCatchBasic {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Index không hợp lệ!");
        }
        
        System.out.println("Chương trình tiếp tục...");
    }
}
````
### 2. Multiple Catch Blocks
````java
public class MultipleCatch {
    public static void main(String[] args) {
        try {
            String text = args[0];  // Có thể gây ArrayIndexOutOfBoundsException
            int number = Integer.parseInt(text);  // Có thể gây NumberFormatException
            int result = 100 / number;  // Có thể gây ArithmeticException
            System.out.println("Kết quả: " + result);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Lỗi: Chưa truyền tham số dòng lệnh!");
        } catch (NumberFormatException e) {
            System.out.println("Lỗi: Tham số phải là số!");
        } catch (ArithmeticException e) {
            System.out.println("Lỗi: Không thể chia cho 0!");
        }
    }
}
````
### 3. Multi-Catch (Java 7+)
```` java
public class MultiCatch {
    public static void main(String[] args) {
        try {
            String text = args[0];
            int number = Integer.parseInt(text);
            int result = 100 / number;
            System.out.println("Kết quả: " + result);
        } catch (ArrayIndexOutOfBoundsException | NumberFormatException e) {
            System.out.println("Lỗi đầu vào: " + e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println("Lỗi tính toán: " + e.getMessage());
        }
    }
}
````
### 4. Finally Block
Block finally luôn được thực thi, dù có exception hay không. Thường dùng để dọn dẹp tài nguyên.
```` java
import java.io.*;

public class FinallyDemo {
    public static void main(String[] args) {
        FileReader reader = null;
        
        try {
            reader = new FileReader("data.txt");
            System.out.println("Đang đọc file...");
            // Code đọc file
        } catch (FileNotFoundException e) {
            System.out.println("Không tìm thấy file!");
        } finally {
            // Finally LUÔN chạy, dù có lỗi hay không
            System.out.println("Đóng tài nguyên...");
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    System.out.println("Lỗi khi đóng file!");
                }
            }
        }
        
        System.out.println("Chương trình kết thúc");
    }
}
````
### 5. Try-with-Resources (Java 7+)
Tự động đóng tài nguyên, không cần finally.
```` java
import java.io.*;

public class TryWithResources {
    public static void main(String[] args) {
        // Tự động đóng reader khi kết thúc try block
        try (FileReader reader = new FileReader("data.txt");
             BufferedReader br = new BufferedReader(reader)) {
            
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
            
        } catch (FileNotFoundException e) {
            System.out.println("Không tìm thấy file!");
        } catch (IOException e) {
            System.out.println("Lỗi đọc file!");
        }
        // Không cần finally, reader được đóng tự động
    }
}
````
<div style="background: #fff3cd; border-left: 5px solid #ffc107; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">⚠️</span>
    <strong style="font-size: 18px; color: #856404;">Cảnh báo</strong>
  </div>
  <p style="margin: 0; color: #856404; line-height: 1.6;"><strong>KHÔNG BAO GIỜ để block catch rỗng!</strong> Empty catch block che giấu bugs và khiến debugging trở nên cực kỳ khó khăn. Ít nhất phải log exception hoặc rethrow nó. Code như <code>catch(Exception e) {}</code> là <strong>bad practice nghiêm trọng</strong>!</p>
</div>

## Throw và Throws
### 1. Throw - Ném Exception
Dùng để chủ động ném một exception.
```` java
public class ThrowDemo {
    public static void checkAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Tuổi phải >= 18!");
        }
        System.out.println("Tuổi hợp lệ: " + age);
    }
    
    public static void main(String[] args) {
        try {
            checkAge(15);
        } catch (IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
    }
}
````
### 2. Throws - Khai báo Exception
Dùng để khai báo rằng method có thể ném exception.
````java
import java.io.*;

public class ThrowsDemo {
    // Method này khai báo có thể ném IOException
    public static void readFile(String filename) throws IOException {
        FileReader reader = new FileReader(filename);
        System.out.println("Đọc file thành công");
        reader.close();
    }
    
    public static void main(String[] args) {
        // Method gọi phải xử lý exception
        try {
            readFile("data.txt");
        } catch (IOException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
    }
}
````
<div style="background: #d4edda; border-left: 5px solid #28a745; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">✅</span>
    <strong style="font-size: 18px; color: #155724;">Best Practice</strong>
  </div>
  <p style="margin: 0; color: #155724; line-height: 1.6;">Khi tạo custom exceptions, kế thừa từ <code>Exception</code> (checked) cho recoverable errors hoặc <code>RuntimeException</code> (unchecked) cho programming errors. Luôn cung cấp constructor với message để dễ debug: <code>throw new CustomException("Detailed error message")</code></p>
</div>

## Custom Exception - Tạo Exception riêng
### Ví dụ 1: Custom Checked Exception
```` java
// Tạo custom exception
class InsufficientBalanceException extends Exception {
    private double amount;
    
    public InsufficientBalanceException(double amount) {
        super("Số dư không đủ. Thiếu: " + amount + "đ");
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}

// Sử dụng custom exception
class BankAccount {
    private String accountNumber;
    private double balance;
    
    public BankAccount(String accountNumber, double balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }
    
    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            double shortage = amount - balance;
            throw new InsufficientBalanceException(shortage);
        }
        balance -= amount;
        System.out.println("Rút " + amount + "đ thành công. Số dư: " + balance + "đ");
    }
    
    public double getBalance() {
        return balance;
    }
}

public class CustomExceptionDemo {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("123456", 1000000);
        
        try {
            System.out.println("Số dư ban đầu: " + account.getBalance() + "đ");
            account.withdraw(500000);   // OK
            account.withdraw(800000);   // Lỗi - không đủ tiền
        } catch (InsufficientBalanceException e) {
            System.out.println("Lỗi: " + e.getMessage());
            System.out.println("Bạn thiếu: " + e.getAmount() + "đ");
        }
    }
}
````

**Output:**
````
Số dư ban đầu: 1000000.0đ
Rút 500000.0đ thành công. Số dư: 500000.0đ
Lỗi: Số dư không đủ. Thiếu: 300000.0đ
Bạn thiếu: 300000.0đ
````
### Ví dụ 2: Custom Unchecked Exception
```` java
// Custom runtime exception
class InvalidEmailException extends RuntimeException {
    public InvalidEmailException(String email) {
        super("Email không hợp lệ: " + email);
    }
}

class User {
    private String name;
    private String email;
    
    public User(String name, String email) {
        this.name = name;
        setEmail(email);
    }
    
    public void setEmail(String email) {
        if (!email.contains("@")) {
            throw new InvalidEmailException(email);
        }
        this.email = email;
    }
    
    @Override
    public String toString() {
        return "User{name='" + name + "', email='" + email + "'}";
    }
}

public class CustomRuntimeExceptionDemo {
    public static void main(String[] args) {
        try {
            User user1 = new User("An", "an@gmail.com");
            System.out.println(user1);
            
            User user2 = new User("Binh", "binh.gmail.com");  // Lỗi
            System.out.println(user2);
        } catch (InvalidEmailException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
    }
}
````
### Exception Chaining
Exception chaining cho phép gắn một exception là nguyên nhân của exception khác.
```` java
class DatabaseException extends Exception {
    public DatabaseException(String message, Throwable cause) {
        super(message, cause);
    }
}

public class ExceptionChaining {
    public static void connectDatabase() throws DatabaseException {
        try {
            // Giả lập kết nối database
            throw new java.sql.SQLException("Không thể kết nối database");
        } catch (java.sql.SQLException e) {
            // Wrap exception gốc vào custom exception
            throw new DatabaseException("Lỗi kết nối hệ thống", e);
        }
    }
    
    public static void main(String[] args) {
        try {
            connectDatabase();
        } catch (DatabaseException e) {
            System.out.println("Lỗi: " + e.getMessage());
            System.out.println("Nguyên nhân: " + e.getCause());
        }
    }
}
````
## Best Practices - Cách viết tốt
### 1. Bắt exception cụ thể
```` java
// ❌ KHÔNG TỐT - Bắt quá chung
try {
    // code
} catch (Exception e) {
    System.out.println("Có lỗi xảy ra");
}

// ✅ TỐT - Bắt cụ thể
try {
    int result = Integer.parseInt(input);
} catch (NumberFormatException e) {
    System.out.println("Input phải là số: " + e.getMessage());
}
````
### 2. Không bỏ trống catch block
```` java
// ❌ SAI - Nuốt exception
try {
    riskyOperation();
} catch (Exception e) {
    // Không làm gì cả - RẤT NGUY HIỂM!
}

// ✅ ĐÚNG - Ít nhất phải log
try {
    riskyOperation();
} catch (Exception e) {
    System.err.println("Lỗi: " + e.getMessage());
    e.printStackTrace();
}
````
### 3. Đóng tài nguyên đúng cách
```` java
// ❌ Không tốt
FileReader reader = null;
try {
    reader = new FileReader("file.txt");
    // đọc file
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// ✅ TỐT HƠN - Try-with-resources
try (FileReader reader = new FileReader("file.txt")) {
    // đọc file
} catch (IOException e) {
    e.printStackTrace();
}
````
### 4. Throw sớm, catch muộn
```` java
// ✅ TỐT - Kiểm tra và throw sớm
public void processUser(User user) {
    if (user == null) {
        throw new IllegalArgumentException("User không được null");
    }
    if (user.getAge() < 0) {
        throw new IllegalArgumentException("Tuổi phải >= 0");
    }
    // Xử lý logic
}

// Catch ở level cao nhất có thể xử lý
public static void main(String[] args) {
    try {
        processUser(user);
    } catch (IllegalArgumentException e) {
        System.out.println("Dữ liệu không hợp lệ: " + e.getMessage());
    }
}
````
### 5. Thông báo lỗi có ý nghĩa
````java
// ❌ Thông báo không rõ ràng
throw new Exception("Lỗi");

// ✅ Thông báo chi tiết
throw new IllegalArgumentException(
    "Tuổi phải từ 18-65. Giá trị nhận được: " + age
);
````
### 6. Không dùng exception cho flow control
````java
// ❌ SAI - Dùng exception để điều khiển luồng
try {
    int i = 0;
    while (true) {
        System.out.println(array[i++]);
    }
} catch (ArrayIndexOutOfBoundsException e) {
    // Dùng exception để thoát vòng lặp - SAI!
}

// ✅ ĐÚNG - Dùng điều kiện bình thường
for (int i = 0; i < array.length; i++) {
    System.out.println(array[i]);
}
````
## Các Exception phổ biến
### 1. NullPointerException
```` java
public class NullPointerDemo {
    public static void main(String[] args) {
        String text = null;
        
        try {
            System.out.println(text.length());  // NPE!
        } catch (NullPointerException e) {
            System.out.println("Lỗi: Biến là null!");
        }
        
        // Cách tránh NPE
        if (text != null) {
            System.out.println(text.length());
        }
        
        // Hoặc dùng Optional (Java 8+)
        String result = text != null ? text : "default";
        System.out.println(result);
    }
}
````
### 2. ClassCastException
```` java
public class ClassCastDemo {
    public static void main(String[] args) {
        Object obj = "Hello";
        
        try {
            Integer num = (Integer) obj;  // Lỗi cast!
        } catch (ClassCastException e) {
            System.out.println("Lỗi: Không thể cast String sang Integer!");
        }
        
        // Cách an toàn với instanceof
        if (obj instanceof Integer) {
            Integer num = (Integer) obj;
        } else {
            System.out.println("obj không phải Integer");
        }
    }
}
````
### 3. IOException khi làm việc với File
```` java
import java.io.*;
import java.util.*;

public class FileExceptionDemo {
    public static void readFile(String filename) {
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("Không tìm thấy file: " + filename);
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
    }
    
    public static void writeFile(String filename, List<String> lines) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            for (String line : lines) {
                writer.write(line);
                writer.newLine();
            }
            System.out.println("Ghi file thành công!");
        } catch (IOException e) {
            System.out.println("Lỗi ghi file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        // Đọc file
        readFile("data.txt");
        
        // Ghi file
        List<String> lines = Arrays.asList("Dòng 1", "Dòng 2", "Dòng 3");
        writeFile("output.txt", lines);
    }
}
````
## Ví dụ thực tế
### Ví dụ 1: Hệ thống đăng nhập
````java
class AuthenticationException extends Exception {
    public AuthenticationException(String message) {
        super(message);
    }
}

class LoginSystem {
    private Map<String, String> users = new HashMap<>();
    
    public LoginSystem() {
        // Dữ liệu mẫu
        users.put("admin", "admin123");
        users.put("user1", "pass123");
    }
    
    public void login(String username, String password) throws AuthenticationException {
        if (username == null || username.isEmpty()) {
            throw new AuthenticationException("Username không được để trống");
        }
        
        if (password == null || password.isEmpty()) {
            throw new AuthenticationException("Password không được để trống");
        }
        
        if (!users.containsKey(username)) {
            throw new AuthenticationException("Username không tồn tại");
        }
        
        if (!users.get(username).equals(password)) {
            throw new AuthenticationException("Sai mật khẩu");
        }
        
        System.out.println("Đăng nhập thành công! Xin chào " + username);
    }
}

public class LoginDemo {
    public static void main(String[] args) {
        LoginSystem system = new LoginSystem();
        Scanner scanner = new Scanner(System.in);
        
        try {
            System.out.print("Username: ");
            String username = scanner.nextLine();
            
            System.out.print("Password: ");
            String password = scanner.nextLine();
            
            system.login(username, password);
            
        } catch (AuthenticationException e) {
            System.out.println("Lỗi đăng nhập: " + e.getMessage());
        } finally {
            scanner.close();
        }
    }
}
````
### Ví dụ 2: Quản lý sản phẩm
````java
import java.util.*;

class ProductNotFoundException extends Exception {
    public ProductNotFoundException(String productId) {
        super("Không tìm thấy sản phẩm: " + productId);
    }
}

class Product {
    private String id;
    private String name;
    private double price;
    private int quantity;
    
    public Product(String id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }
    
    public String getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
    public void setQuantity(int quantity) { this.quantity = quantity; }
    
    @Override
    public String toString() {
        return String.format("%s - %s: %.0fđ (SL: %d)", id, name, price, quantity);
    }
}

class ProductManager {
    private List<Product> products = new ArrayList<>();
    
    public ProductManager() {
        // Dữ liệu mẫu
        products.add(new Product("P001", "Laptop", 15000000, 10));
        products.add(new Product("P002", "Mouse", 200000, 50));
        products.add(new Product("P003", "Keyboard", 500000, 30));
    }
    
    public Product findProduct(String id) throws ProductNotFoundException {
        for (Product p : products) {
            if (p.getId().equals(id)) {
                return p;
            }
        }
        throw new ProductNotFoundException(id);
    }
    
    public void buyProduct(String id, int quantity) 
            throws ProductNotFoundException, IllegalArgumentException {
        
        if (quantity <= 0) {
            throw new IllegalArgumentException("Số lượng phải > 0");
        }
        
        Product product = findProduct(id);
        
        if (product.getQuantity() < quantity) {
            throw new IllegalArgumentException(
                "Không đủ hàng. Còn lại: " + product.getQuantity()
            );
        }
        
        product.setQuantity(product.getQuantity() - quantity);
        double total = product.getPrice() * quantity;
        
        System.out.println("Mua thành công!");
        System.out.println("Sản phẩm: " + product.getName());
        System.out.println("Số lượng: " + quantity);
        System.out.println("Tổng tiền: " + total + "đ");
    }
    
    public void listProducts() {
        System.out.println("=== DANH SÁCH SẢN PHẨM ===");
        for (Product p : products) {
            System.out.println(p);
        }
    }
}

public class ProductDemo {
    public static void main(String[] args) {
        ProductManager manager = new ProductManager();
        manager.listProducts();
        
        System.out.println("\n=== MUA HÀNG ===");
        
        // Test case 1: Mua thành công
        try {
            System.out.println("\nTest 1: Mua 2 Laptop");
            manager.buyProduct("P001", 2);
        } catch (ProductNotFoundException | IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 2: Sản phẩm không tồn tại
        try {
            System.out.println("\nTest 2: Mua sản phẩm không tồn tại");
            manager.buyProduct("P999", 1);
        } catch (ProductNotFoundException | IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 3: Số lượng không hợp lệ
        try {
            System.out.println("\nTest 3: Mua số lượng âm");
            manager.buyProduct("P002", -5);
        } catch (ProductNotFoundException | IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 4: Không đủ hàng
        try {
            System.out.println("\nTest 4: Mua quá số lượng tồn kho");
            manager.buyProduct("P002", 100);
        } catch (ProductNotFoundException | IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        System.out.println("\n=== DANH SÁCH SAU KHI MUA ===");
        manager.listProducts();
    }
}
````

**Output:**
````
=== DANH SÁCH SẢN PHẨM ===
P001 - Laptop: 15000000đ (SL: 10)
P002 - Mouse: 200000đ (SL: 50)
P003 - Keyboard: 500000đ (SL: 30)

=== MUA HÀNG ===

Test 1: Mua 2 Laptop
Mua thành công!
Sản phẩm: Laptop
Số lượng: 2
Tổng tiền: 30000000.0đ

Test 2: Mua sản phẩm không tồn tại
Lỗi: Không tìm thấy sản phẩm: P999

Test 3: Mua số lượng âm
Lỗi: Số lượng phải > 0

Test 4: Mua quá số lượng tồn kho
Lỗi: Không đủ hàng. Còn lại: 50

=== DANH SÁCH SAU KHI MUA ===
P001 - Laptop: 15000000đ (SL: 8)
P002 - Mouse: 200000đ (SL: 50)
P003 - Keyboard: 500000đ (SL: 30)
````
### Ví dụ 3: Xử lý dữ liệu sinh viên
```` java
import java.util.*;

class InvalidScoreException extends Exception {
    public InvalidScoreException(double score) {
        super("Điểm không hợp lệ: " + score + ". Điểm phải từ 0-10");
    }
}

class DuplicateStudentException extends Exception {
    public DuplicateStudentException(String studentId) {
        super("Sinh viên đã tồn tại: " + studentId);
    }
}

class Student {
    private String id;
    private String name;
    private double score;
    
    public Student(String id, String name, double score) throws InvalidScoreException {
        this.id = id;
        this.name = name;
        setScore(score);
    }
    
    public void setScore(double score) throws InvalidScoreException {
        if (score < 0 || score > 10) {
            throw new InvalidScoreException(score);
        }
        this.score = score;
    }
    
    public String getId() { return id; }
    public String getName() { return name; }
    public double getScore() { return score; }
    
    public String getGrade() {
        if (score >= 9.0) return "Xuất sắc";
        if (score >= 8.0) return "Giỏi";
        if (score >= 7.0) return "Khá";
        if (score >= 5.0) return "Trung bình";
        return "Yếu";
    }
    
    @Override
    public String toString() {
        return String.format("%s - %s: %.1f (%s)", id, name, score, getGrade());
    }
}

class StudentManager {
    private List<Student> students = new ArrayList<>();
    
    public void addStudent(Student student) throws DuplicateStudentException {
        // Kiểm tra trùng lặp
        for (Student s : students) {
            if (s.getId().equals(student.getId())) {
                throw new DuplicateStudentException(student.getId());
            }
        }
        students.add(student);
        System.out.println("Thêm sinh viên thành công: " + student);
    }
    
    public Student findStudent(String id) throws ProductNotFoundException {
        for (Student s : students) {
            if (s.getId().equals(id)) {
                return s;
            }
        }
        throw new ProductNotFoundException(id);
    }
    
    public void updateScore(String id, double newScore) 
            throws ProductNotFoundException, InvalidScoreException {
        Student student = findStudent(id);
        student.setScore(newScore);
        System.out.println("Cập nhật điểm thành công: " + student);
    }
    
    public void displayAllStudents() {
        if (students.isEmpty()) {
            System.out.println("Danh sách trống!");
            return;
        }
        
        System.out.println("\n=== DANH SÁCH SINH VIÊN ===");
        for (Student s : students) {
            System.out.println(s);
        }
    }
    
    public void displayStatistics() {
        if (students.isEmpty()) {
            System.out.println("Không có dữ liệu!");
            return;
        }
        
        double sum = 0;
        double max = students.get(0).getScore();
        double min = students.get(0).getScore();
        
        for (Student s : students) {
            double score = s.getScore();
            sum += score;
            if (score > max) max = score;
            if (score < min) min = score;
        }
        
        double avg = sum / students.size();
        
        System.out.println("\n=== THỐNG KÊ ===");
        System.out.println("Tổng số sinh viên: " + students.size());
        System.out.printf("Điểm trung bình: %.2f\n", avg);
        System.out.printf("Điểm cao nhất: %.1f\n", max);
        System.out.printf("Điểm thấp nhất: %.1f\n", min);
    }
}

public class StudentDemo {
    public static void main(String[] args) {
        StudentManager manager = new StudentManager();
        
        System.out.println("=== THÊM SINH VIÊN ===");
        
        // Test case 1: Thêm sinh viên hợp lệ
        try {
            manager.addStudent(new Student("SV001", "Nguyễn Văn An", 8.5));
            manager.addStudent(new Student("SV002", "Trần Thị Bình", 7.0));
            manager.addStudent(new Student("SV003", "Lê Văn Chính", 9.5));
        } catch (InvalidScoreException | DuplicateStudentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 2: Thêm sinh viên với điểm không hợp lệ
        try {
            System.out.println("\nTest: Thêm SV với điểm không hợp lệ");
            manager.addStudent(new Student("SV004", "Phạm Văn Dũng", 11.0));
        } catch (InvalidScoreException | DuplicateStudentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 3: Thêm sinh viên trùng ID
        try {
            System.out.println("\nTest: Thêm SV trùng ID");
            manager.addStudent(new Student("SV001", "Hoàng Văn E", 8.0));
        } catch (InvalidScoreException | DuplicateStudentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Hiển thị danh sách
        manager.displayAllStudents();
        
        // Test case 4: Cập nhật điểm
        try {
            System.out.println("\n=== CẬP NHẬT ĐIỂM ===");
            manager.updateScore("SV001", 9.0);
        } catch (ProductNotFoundException | InvalidScoreException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 5: Cập nhật điểm không hợp lệ
        try {
            System.out.println("\nTest: Cập nhật điểm không hợp lệ");
            manager.updateScore("SV002", -5.0);
        } catch (ProductNotFoundException | InvalidScoreException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Hiển thị danh sách sau cập nhật
        manager.displayAllStudents();
        
        // Thống kê
        manager.displayStatistics();
    }
}
````
---

## 🐛 Lỗi thường gặp với Exception Handling

### ❌ Lỗi 1: Empty Catch Block

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Swallowing Exceptions</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Empty catch block "nuốt" exception mà không xử lý gì - lỗi nghiêm trọng nhất trong exception handling!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ CỰC KỲ TỆ - Che giấu bugs!
try {
    int result = 10 / 0;
    System.out.println(result);
} catch (Exception e) {
    // RỖNG - Không làm gì cả!
}
// Chương trình tiếp tục như không có gì xảy ra
```

**Tại sao tệ?**
- ❌ Không biết có lỗi xảy ra
- ❌ Debugging cực kỳ khó
- ❌ Production bugs không thể phát hiện

**Cách fix:**
```java
// ✅ ĐÚNG - Ít nhất phải log
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.err.println("Error: " + e.getMessage());
    e.printStackTrace();
    // Hoặc log với logging framework
}

// ✅ HOẶC - Rethrow nếu không xử lý được
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Operation failed", e);
    throw e;  // Rethrow để caller xử lý
}
```

---

### ❌ Lỗi 2: Catch Exception quá chung

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Overly Broad Catch</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Catch <code>Exception</code> hoặc <code>Throwable</code> quá chung, bắt cả những lỗi không nên catch!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - Quá chung!
try {
    readFile("data.txt");
    int result = calculateData();
    saveToDatabase(result);
} catch (Exception e) {  // Bắt MỌI exception!
    System.out.println("Something went wrong");
    // Không biết lỗi gì: file không tồn tại? calculation error? database down?
}
```

**Cách fix:**
```java
// ✅ ĐÚNG - Catch cụ thể
try {
    readFile("data.txt");
    int result = calculateData();
    saveToDatabase(result);
} catch (FileNotFoundException e) {
    System.err.println("File not found: " + e.getMessage());
} catch (ArithmeticException e) {
    System.err.println("Calculation error: " + e.getMessage());
} catch (SQLException e) {
    System.err.println("Database error: " + e.getMessage());
}
```

---

### ❌ Lỗi 3: Không đóng resources

<div style="background: #f8d7da; border-left: 5px solid #dc3545; padding: 20px; margin: 25px 0; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
    <span style="font-size: 24px;">❌</span>
    <strong style="font-size: 18px; color: #721c24;">Resource Leak</strong>
  </div>
  <p style="margin: 0; color: #721c24; line-height: 1.6;">Quên đóng files, connections, streams → memory leak và resource exhaustion!</p>
</div>

**Ví dụ SAI:**
```java
// ❌ SAI - File không được đóng nếu có exception
FileReader reader = new FileReader("data.txt");
BufferedReader br = new BufferedReader(reader);
String line = br.readLine();
br.close();  // Không chạy nếu readLine() throw exception!
```

**Cách fix:**
```java
// ✅ ĐÚNG - Dùng try-with-resources (Java 7+)
try (FileReader reader = new FileReader("data.txt");
     BufferedReader br = new BufferedReader(reader)) {
    String line = br.readLine();
    // Resources tự động đóng, kể cả khi có exception!
} catch (IOException e) {
    System.err.println("IO Error: " + e.getMessage());
}

// ✅ HOẶC - finally block (Java 6 trở xuống)
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("data.txt"));
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (br != null) {
        try {
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
---

## 📝 Kiểm tra kiến thức

<div style="background: #f8f9fa; padding: 25px; border-radius: 12px; margin: 30px 0; border: 2px solid #e9ecef;">

**Câu 1:** Checked Exception vs Unchecked Exception?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>✅ Checked Exception:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Kế thừa từ <code>Exception</code> (không phải RuntimeException)</li>
      <li>Compiler <strong>BẮT BUỘC</strong> phải handle (try-catch hoặc throws)</li>
      <li>Ví dụ: <code>IOException</code>, <code>SQLException</code>, <code>FileNotFoundException</code></li>
      <li>📌 Dùng cho: Recoverable errors (có thể xử lý được)</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>⚡ Unchecked Exception:</strong></p>
    <ul style="margin: 0;">
      <li>Kế thừa từ <code>RuntimeException</code></li>
      <li>Compiler <strong>KHÔNG BẮT</strong> phải handle</li>
      <li>Ví dụ: <code>NullPointerException</code>, <code>ArrayIndexOutOfBoundsException</code></li>
      <li>📌 Dùng cho: Programming errors (bugs trong code)</li>
    </ul>
  </div>
</details>

**Câu 2:** throw vs throws - Khác nhau gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <table style="width: 100%; border-collapse: collapse;">
      <tr style="background: #f8f9fa;">
        <th style="padding: 10px; border: 1px solid #dee2e6;">Tiêu chí</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">throw</th>
        <th style="padding: 10px; border: 1px solid #dee2e6;">throws</th>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Vị trí</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Trong method body</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Trong method signature</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Công dụng</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Ném exception</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Khai báo có thể throw</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Số lượng</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">1 exception</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Nhiều exceptions</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #dee2e6;">Ví dụ</td>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><code>throw new IOException();</code></td>
        <td style="padding: 10px; border: 1px solid #dee2e6;"><code>throws IOException, SQLException</code></td>
      </tr>
    </table>
  </div>
</details>

**Câu 3:** Finally block có LUÔN chạy không?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>✅ CÓ - finally luôn chạy</strong> (hầu hết trường hợp)</p>
    <p style="margin: 0 0 10px 0;"><strong>❌ Trừ khi:</strong></p>
    <ul style="margin: 0;">
      <li><code>System.exit()</code> được gọi</li>
      <li>JVM crash</li>
      <li>Thread bị kill</li>
      <li>Fatal error (OutOfMemoryError, StackOverflowError)</li>
    </ul>
    <p style="margin: 15px 0 0 0; padding: 10px; background: #e3f2fd; border-radius: 4px;">💡 finally chạy kể cả khi có <code>return</code> trong try/catch!</p>
  </div>
</details>

**Câu 4:** Try-with-resources là gì?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;">Try-with-resources (Java 7+) tự động đóng resources sau khi dùng xong:</p>
    <pre style="background: #f5f5f5; padding: 10px; border-radius: 4px; margin: 10px 0;"><code>try (FileReader fr = new FileReader("file.txt")) {
    // Dùng fr
} // fr tự động close() ở đây!</code></pre>
    <p style="margin: 10px 0 0 0;"><strong>Yêu cầu:</strong> Resource phải implement <code>AutoCloseable</code> interface</p>
  </div>
</details>

**Câu 5:** Khi nào NÊN throw exception, khi nào NÊN catch?

<details style="margin: 15px 0; cursor: pointer;">
  <summary style="font-weight: 600; color: #4CAF50; padding: 10px; background: white; border-radius: 6px; border: 1px solid #e9ecef;">👉 Click để xem đáp án</summary>
  <div style="padding: 15px; margin-top: 10px; background: white; border-radius: 6px; border-left: 4px solid #4CAF50;">
    <p style="margin: 0 0 10px 0;"><strong>🎯 Throw khi:</strong></p>
    <ul style="margin: 0 0 15px 0;">
      <li>Method không thể xử lý lỗi</li>
      <li>Muốn caller biết và xử lý</li>
      <li>Validate input và phát hiện invalid data</li>
    </ul>
    <p style="margin: 0 0 10px 0;"><strong>🛡️ Catch khi:</strong></p>
    <ul style="margin: 0;">
      <li>Có thể recover từ lỗi</li>
      <li>Muốn log và tiếp tục chạy</li>
      <li>Ở layer cao nhất (UI, API endpoint)</li>
    </ul>
  </div>
</details>

</div>

## Bài tập thực hành
### Bài 1: Máy tính đơn giản
````java
// Yêu cầu: Viết chương trình máy tính với các phép tính cơ bản
// Xử lý các exception: chia cho 0, input không hợp lệ

import java.util.Scanner;

class CalculatorException extends Exception {
    public CalculatorException(String message) {
        super(message);
    }
}

class Calculator {
    public double calculate(double a, double b, String operator) 
            throws CalculatorException {
        
        switch (operator) {
            case "+":
                return a + b;
            case "-":
                return a - b;
            case "*":
                return a * b;
            case "/":
                if (b == 0) {
                    throw new CalculatorException("Không thể chia cho 0");
                }
                return a / b;
            default:
                throw new CalculatorException("Phép tính không hợp lệ: " + operator);
        }
    }
}

public class CalculatorDemo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Calculator calc = new Calculator();
        
        try {
            System.out.print("Nhập số thứ nhất: ");
            double a = Double.parseDouble(scanner.nextLine());
            
            System.out.print("Nhập phép tính (+, -, *, /): ");
            String operator = scanner.nextLine();
            
            System.out.print("Nhập số thứ hai: ");
            double b = Double.parseDouble(scanner.nextLine());
            
            double result = calc.calculate(a, b, operator);
            System.out.printf("Kết quả: %.2f %s %.2f = %.2f\n", a, operator, b, result);
            
        } catch (NumberFormatException e) {
            System.out.println("Lỗi: Vui lòng nhập số hợp lệ!");
        } catch (CalculatorException e) {
            System.out.println("Lỗi: " + e.getMessage());
        } finally {
            scanner.close();
        }
    }
}
````
### Bài 2: Quản lý thư viện
````java
// Yêu cầu: Tạo hệ thống quản lý mượn/trả sách
// Xử lý: sách không tồn tại, đã được mượn, v.v.

import java.util.*;

class BookNotAvailableException extends Exception {
    public BookNotAvailableException(String bookTitle) {
        super("Sách đang được mượn: " + bookTitle);
    }
}

class BookNotFoundException extends Exception {
    public BookNotFoundException(String bookTitle) {
        super("Không tìm thấy sách: " + bookTitle);
    }
}

class Book {
    private String title;
    private String author;
    private boolean isAvailable;
    
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
        this.isAvailable = true;
    }
    
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
    public boolean isAvailable() { return isAvailable; }
    public void setAvailable(boolean available) { this.isAvailable = available; }
    
    @Override
    public String toString() {
        String status = isAvailable ? "Có sẵn" : "Đang mượn";
        return String.format("'%s' - %s [%s]", title, author, status);
    }
}

class Library {
    private List<Book> books = new ArrayList<>();
    
    public Library() {
        // Dữ liệu mẫu
        books.add(new Book("Java Programming", "John Doe"));
        books.add(new Book("Clean Code", "Robert Martin"));
        books.add(new Book("Design Patterns", "Gang of Four"));
    }
    
    public Book findBook(String title) throws BookNotFoundException {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title)) {
                return book;
            }
        }
        throw new BookNotFoundException(title);
    }
    
    public void borrowBook(String title) 
            throws BookNotFoundException, BookNotAvailableException {
        
        Book book = findBook(title);
        
        if (!book.isAvailable()) {
            throw new BookNotAvailableException(title);
        }
        
        book.setAvailable(false);
        System.out.println("Mượn sách thành công: " + book.getTitle());
    }
    
    public void returnBook(String title) throws BookNotFoundException {
        Book book = findBook(title);
        
        if (book.isAvailable()) {
            System.out.println("Sách này chưa được mượn!");
            return;
        }
        
        book.setAvailable(true);
        System.out.println("Trả sách thành công: " + book.getTitle());
    }
    
    public void displayBooks() {
        System.out.println("\n=== DANH SÁCH SÁCH ===");
        for (Book book : books) {
            System.out.println(book);
        }
    }
}

public class LibraryDemo {
    public static void main(String[] args) {
        Library library = new Library();
        library.displayBooks();
        
        System.out.println("\n=== MƯỢN SÁCH ===");
        
        // Test case 1: Mượn sách thành công
        try {
            library.borrowBook("Java Programming");
        } catch (BookNotFoundException | BookNotAvailableException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 2: Mượn sách đã được mượn
        try {
            library.borrowBook("Java Programming");
        } catch (BookNotFoundException | BookNotAvailableException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 3: Mượn sách không tồn tại
        try {
            library.borrowBook("Python Programming");
        } catch (BookNotFoundException | BookNotAvailableException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        library.displayBooks();
        
        System.out.println("\n=== TRẢ SÁCH ===");
        
        // Test case 4: Trả sách
        try {
            library.returnBook("Java Programming");
        } catch (BookNotFoundException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        library.displayBooks();
    }
}
````
### Bài 3: Validation dữ liệu người dùng

```` java
// Yêu cầu: Validate thông tin đăng ký người dùng
// Username, email, password phải đúng format

class ValidationException extends Exception {
    public ValidationException(String message) {
        super(message);
    }
}

class UserValidator {
    public static void validateUsername(String username) throws ValidationException {
        if (username == null || username.isEmpty()) {
            throw new ValidationException("Username không được để trống");
        }
        if (username.length() < 5) {
            throw new ValidationException("Username phải có ít nhất 5 ký tự");
        }
        if (!username.matches("^[a-zA-Z0-9_]+$")) {
            throw new ValidationException("Username chỉ chứa chữ, số và _");
        }
    }
    
    public static void validateEmail(String email) throws ValidationException {
        if (email == null || email.isEmpty()) {
            throw new ValidationException("Email không được để trống");
        }
        if (!email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$")) {
            throw new ValidationException("Email không đúng định dạng");
        }
    }
    
    public static void validatePassword(String password) throws ValidationException {
        if (password == null || password.isEmpty()) {
            throw new ValidationException("Password không được để trống");
        }
        if (password.length() < 8) {
            throw new ValidationException("Password phải có ít nhất 8 ký tự");
        }
        if (!password.matches(".*[A-Z].*")) {
            throw new ValidationException("Password phải có ít nhất 1 chữ hoa");
        }
        if (!password.matches(".*[0-9].*")) {
            throw new ValidationException("Password phải có ít nhất 1 số");
        }
    }
    
    public static void validateAge(int age) throws ValidationException {
        if (age < 18) {
            throw new ValidationException("Tuổi phải >= 18");
        }
        if (age > 100) {
            throw new ValidationException("Tuổi phải <= 100");
        }
    }
}

class UserRegistration {
    private String username;
    private String email;
    private String password;
    private int age;
    
    public UserRegistration(String username, String email, String password, int age) 
            throws ValidationException {
        
        UserValidator.validateUsername(username);
        UserValidator.validateEmail(email);
        UserValidator.validatePassword(password);
        UserValidator.validateAge(age);
        
        this.username = username;
        this.email = email;
        this.password = password;
        this.age = age;
        
        System.out.println("Đăng ký thành công!");
        System.out.println("Username: " + username);
        System.out.println("Email: " + email);
    }
}

public class ValidationDemo {
    public static void main(String[] args) {
        // Test case 1: Đăng ký thành công
        try {
            System.out.println("Test 1: Dữ liệu hợp lệ");
            new UserRegistration("john_doe", "john@gmail.com", "Pass123456", 25);
        } catch (ValidationException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 2: Username quá ngắn
        try {
            System.out.println("\nTest 2: Username quá ngắn");
            new UserRegistration("abc", "test@gmail.com", "Pass123456", 25);
        } catch (ValidationException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 3: Email không hợp lệ
        try {
            System.out.println("\nTest 3: Email không hợp lệ");
            new UserRegistration("john_doe", "invalid-email", "Pass123456", 25);
        } catch (ValidationException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 4: Password yếu
        try {
            System.out.println("\nTest 4: Password yếu");
            new UserRegistration("john_doe", "john@gmail.com", "password", 25);
        } catch (ValidationException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        // Test case 5: Tuổi không hợp lệ
        try {
            System.out.println("\nTest 5: Tuổi < 18");
            new UserRegistration("john_doe", "john@gmail.com", "Pass123456", 15);
        } catch (ValidationException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
    }
}
````
## So sánh: Có và không có Exception Handling
### Ví dụ: Đọc file và parse dữ liệu
❌ Không có Exception Handling:
```` java
public class WithoutExceptionHandling {
    public static void main(String[] args) {
        String filename = "data.txt";
        FileReader reader = new FileReader(filename);  // Compile error!
        
        String text = "100";
        int number = Integer.parseInt(text);
        
        int result = number / 0;  // Runtime error!
        
        System.out.println("Result: " + result);
    }
}
````
Code này thậm chí không compile được!

✅ Có Exception Handling:
````java
import java.io.*;

public class WithExceptionHandling {
    public static void main(String[] args) {
        String filename = "data.txt";
        
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            String line = reader.readLine();
            
            if (line != null) {
                int number = Integer.parseInt(line.trim());
                
                if (number != 0) {
                    int result = 100 / number;
                    System.out.println("Kết quả: " + result);
                } else {
                    System.out.println("Không thể chia cho 0");
                }
            }
            
        } catch (FileNotFoundException e) {
            System.out.println("Không tìm thấy file: " + filename);
            System.out.println("Vui lòng kiểm tra lại đường dẫn!");
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("Dữ liệu trong file không phải số!");
        }
        
        System.out.println("Chương trình kết thúc bình thường");
    }
}
````
## Common Mistakes (Lỗi thường gặp)
### 1. Catch Exception quá chung
````java
// ❌ SAI
try {
    // complex code
} catch (Exception e) {
    e.printStackTrace();  // Bắt mọi exception - không tốt!
}

// ✅ ĐÚNG
try {
    // complex code
} catch (IOException e) {
    // Xử lý lỗi I/O cụ thể
} catch (SQLException e) {
    // Xử lý lỗi database cụ thể
}
````
### 2. Nuốt exception

```` java
// ❌ SAI - Rất nguy hiểm!
try {
    riskyOperation();
} catch (Exception e) {
    // Im lặng - không ai biết có lỗi!
}

// ✅ ĐÚNG
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Error in riskyOperation", e);
    // hoặc ít nhất
    e.printStackTrace();
}
````
### 3. Return trong finally
```` java
// ❌ SAI - Finally override return trong try!
public int badMethod() {
    try {
        return 1;
    } finally {
        return 2;  // Giá trị này sẽ được return!
    }
}

// ✅ ĐÚNG
public int goodMethod() {
    int result = 0;
    try {
        result = 1;
    } finally {
        // Dọn dẹp tài nguyên, không return
    }
    return result;
}
````
### 4. Throw exception trong constructor quá nhiều
````java
// ❌ Không tốt
public class User {
    public User(String name, String email, int age) 
            throws InvalidNameException, InvalidEmailException, InvalidAgeException {
        // Quá nhiều exception!
    }
}

// ✅ Tốt hơn
public class User {
    public User(String name, String email, int age) throws ValidationException {
        // Gộp thành 1 exception duy nhất
        validateAll(name, email, age);
    }
}
````
## Tips nâng cao
### 1. Sử dụng Try-with-Resources cho nhiều tài nguyên
``` java
try (FileInputStream fis = new FileInputStream("input.txt");
     FileOutputStream fos = new FileOutputStream("output.txt");
     BufferedReader reader = new BufferedReader(new InputStreamReader(fis));
     BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(fos))) {
    
    String line;
    while ((line = reader.readLine()) != null) {
        writer.write(line.toUpperCase());
        writer.newLine();
    }
    
} catch (IOException e) {
    System.out.println("Lỗi xử lý file: " + e.getMessage());
}
// Tất cả tài nguyên được đóng tự động theo thứ tự ngược lại
````
### 2. Suppressed Exceptions
````java
public class SuppressedExceptionDemo {
    public static void main(String[] args) {
        try {
            openAndProcess();
        } catch (Exception e) {
            System.out.println("Main exception: " + e.getMessage());
            
            // Kiểm tra suppressed exceptions
            Throwable[] suppressed = e.getSuppressed();
            for (Throwable t : suppressed) {
                System.out.println("Suppressed: " + t.getMessage());
            }
        }
    }
    
    static class Resource implements AutoCloseable {
        private String name;
        
        public Resource(String name) throws Exception {
            this.name = name;
            if (name.equals("Bad")) {
                throw new Exception("Cannot create " + name);
            }
        }
        
        @Override
        public void close() throws Exception {
            throw new Exception("Error closing " + name);
        }
    }
    
    static void openAndProcess() throws Exception {
        try (Resource r1 = new Resource("Good")) {
            throw new Exception("Processing error");
        }
        // Close exception sẽ bị suppressed
    }
}
````
### 3. Custom Exception Hierarchy
```` java
// Base exception
class ApplicationException extends Exception {
    public ApplicationException(String message) {
        super(message);
    }
    
    public ApplicationException(String message, Throwable cause) {
        super(message, cause);
    }
}

// Specific exceptions
class DataException extends ApplicationException {
    public DataException(String message) {
        super(message);
    }
}

class NetworkException extends ApplicationException {
    public NetworkException(String message) {
        super(message);
    }
}

class ValidationException extends ApplicationException {
    public ValidationException(String message) {
        super(message);
    }
}

// Sử dụng
public class ExceptionHierarchyDemo {
    public static void main(String[] args) {
        try {
            processData();
        } catch (DataException e) {
            System.out.println("Lỗi dữ liệu: " + e.getMessage());
        } catch (NetworkException e) {
            System.out.println("Lỗi mạng: " + e.getMessage());
        } catch (ApplicationException e) {
            System.out.println("Lỗi ứng dụng: " + e.getMessage());
        }
    }
    
    static void processData() throws ApplicationException {
        // Implementation
    }
}
````
## Kết luận
“Nắm vững cơ chế xử lý ngoại lệ giúp lập trình viên viết chương trình an toàn, ổn định hơn. Exception Handling cũng là nền tảng cho nhiều framework như Spring Boot, nơi việc xử lý lỗi được tổ chức có hệ thống.” Nó giúp:
### ✅ Lợi ích chính:

#### Tăng độ tin cậy: Chương trình không bị crash đột ngột
#### Dễ debug: Thông báo lỗi rõ ràng, stack trace chi tiết
#### Code sạch hơn: Tách biệt logic xử lý lỗi khỏi logic nghiệp vụ
#### Linh hoạt: Có thể xử lý lỗi ở nhiều level khác nhau
#### Bảo trì tốt: Dễ dàng thêm/sửa xử lý lỗi sau này

### 📌 Những điểm cần nhớ:

#### Checked Exception: Phải xử lý lúc compile-time
#### Unchecked Exception: Không bắt buộc xử lý, thường do lỗi logic
#### Try-Catch-Finally: Cấu trúc xử lý exception cơ bản
#### Try-with-Resources: Tự động đóng tài nguyên (Java 7+)
#### Throw: Ném exception
#### Throws: Khai báo exception trong method signature
#### Custom Exception: Tạo exception riêng cho ứng dụng
#### Best Practices: Catch cụ thể, không nuốt exception, thông báo rõ ràng

### 🎯 Khi nào dùng Exception Handling:

✅ Đọc/ghi file

✅ Kết nối database

✅ Kết nối mạng

✅ Parse dữ liệu

✅ Validate input

✅ Xử lý nghiệp vụ phức tạp

### ⚠️ Khi nào KHÔNG nên dùng:

❌ Để điều khiển luồng chương trình (flow control)

❌ Cho những tình huống có thể kiểm tra trước (như null check)

❌ Trong vòng lặp với performance cao

### 💡 Lời khuyên:

Fail fast: Phát hiện lỗi sớm nhất có thể

Fail safe: Xử lý lỗi một cách an toàn

Log đầy đủ: Ghi lại thông tin lỗi để debug

User-friendly message: Thông báo dễ hiểu cho người dùng

Don't catch if you can't handle: Chỉ catch khi bạn biết cách xử lý

## Tài liệu tham khảo

Oracle Java Documentation - Exceptions

Oracle Java Documentation - Try-with-Resources

Baeldung - Exception Handling in Java

Effective Java by Joshua Bloch - Chapter on
---

## 📚 Bài viết liên quan

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin: 40px 0;">

<a href="/posts/bai2" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">☕</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">Java Collections Framework</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">ArrayList, HashMap, LinkedList trong Java</p>
  </div>
</a>

<a href="/posts/bai3" style="text-decoration: none;">
  <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 25px; border-radius: 12px; transition: transform 0.3s, box-shadow 0.3s; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" onmouseover="this.style.transform='translateY(-5px)'; this.style.boxShadow='0 8px 20px rgba(0,0,0,0.2)'" onmouseout="this.style.transform='translateY(0)'; this.style.boxShadow='0 4px 12px rgba(0,0,0,0.1)'">
    <div style="font-size: 48px; margin-bottom: 15px; color: white;">🏛️</div>
    <h4 style="margin: 0 0 10px 0; color: white; font-size: 20px;">OOP Principles trong Java</h4>
    <p style="margin: 0; color: rgba(255,255,255,0.9); font-size: 14px; line-height: 1.6;">4 nguyên lý OOP</p>
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
