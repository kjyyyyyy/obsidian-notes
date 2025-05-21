在Java中，可以通过 `Scanner` 或 `BufferedReader` 类实现键盘输入。以下是两种方法的详细示例和说明：

---

### **方法一：使用 `Scanner` 类（推荐新手使用）**
`Scanner` 是 Java 提供的便捷工具类，适合简单的输入操作。

```java
import java.util.Scanner; // 必须导入包

public class KeyboardInputExample {
    public static void main(String[] args) {
        // 1. 创建 Scanner 对象，关联键盘输入流 System.in
        Scanner scanner = new Scanner(System.in);

        // 2. 读取不同类型的输入
        System.out.print("请输入一个字符串：");
        String text = scanner.nextLine(); // 读取整行（包括空格）

        System.out.print("请输入一个整数：");
        int number = scanner.nextInt();    // 读取整数

        System.out.print("请输入一个浮点数：");
        double decimal = scanner.nextDouble(); // 读取浮点数

        // 3. 输出结果
        System.out.println("字符串内容: " + text);
        System.out.println("整数内容: " + number);
        System.out.println("浮点数内容: " + decimal);

        // 4. 关闭 Scanner（非必须，但建议释放资源）
        scanner.close();
    }
}
```

**注意事项：**
- `nextLine()` 会读取整行输入（包括空格），而 `next()` 只读取到第一个空格。
- 混合使用 `nextLine()` 和其他 `nextXxx()` 方法时，可能会因换行符残留导致问题。解决方式：在 `nextInt()` 后调用一次 `nextLine()` 清除缓冲区。
- 输入类型不匹配会抛出 `InputMismatchException`，需用 `hasNextInt()` 等方法预先校验。

---

### **方法二：使用 `BufferedReader` 类**
`BufferedReader` 效率更高，适合复杂或大量输入，但代码稍显复杂。

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class KeyboardInputExample {
    public static void main(String[] args) throws IOException {
        // 1. 创建 BufferedReader 对象
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

        // 2. 读取输入（返回字符串，需手动转换类型）
        System.out.print("请输入一个字符串：");
        String text = reader.readLine();

        System.out.print("请输入一个整数：");
        int number = Integer.parseInt(reader.readLine()); // 字符串转整数

        System.out.print("请输入一个浮点数：");
        double decimal = Double.parseDouble(reader.readLine()); // 字符串转浮点数

        // 3. 输出结果
        System.out.println("字符串内容: " + text);
        System.out.println("整数内容: " + number);
        System.out.println("浮点数内容: " + decimal);
    }
}
```

**注意事项：**
- `readLine()` 返回字符串，需手动转换类型（如 `Integer.parseInt()`）。
- 类型转换失败会抛出 `NumberFormatException`，建议用 `try-catch` 处理异常。
- 不需要手动关闭 `BufferedReader`（除非明确需要提前释放资源）。

---

### **常见问题解决**
1. **输入顺序问题**：  
   若 `nextInt()` 后紧跟 `nextLine()`，后者可能读取到空值。  
   **解决方法**：在 `nextInt()` 后添加 `scanner.nextLine()` 清除缓冲区。

2. **异常处理**：  
   使用 `try-catch` 捕获输入错误：
   ```java
   try {
       int num = scanner.nextInt();
   } catch (InputMismatchException e) {
       System.out.println("输入的不是整数！");
       scanner.nextLine(); // 清除错误输入
   }
   ```

---

### **总结**
- **简单输入**：用 `Scanner`（易用，自动类型转换）。
- **高性能或复杂输入**：用 `BufferedReader`（需手动处理类型和异常）。

根据需求选择合适的方法，并注意处理输入边界和异常！