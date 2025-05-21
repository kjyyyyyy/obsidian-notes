![[Pasted image 20250425213136.png]]
在 Java 中，基本数据类型（Primitive Data Types）和引用数据类型（Reference Data Types）的比较方式存在显著差异，主要体现在 **比较的机制** 和 **比较的结果** 上。

---

### **一、基本数据类型的比较**
#### 1. **数据类型**
- 8 种基本类型：`byte`、`short`、`int`、`long`、`float`、`double`、`char`、`boolean`。
- **直接存储值**，变量直接保存数据本身。

#### 2. **比较方式**
- **使用 `==` 比较**：直接比较变量的**值**是否相等。
  ```java
  int a = 5;
  int b = 5;
  System.out.println(a == b); // true（值相同）
  ```

#### 3. **示例**
  ```java
  char c1 = 'A';
  char c2 = 'A';
  System.out.println(c1 == c2); // true（值相同）
  
  double d1 = 3.14;
  double d2 = 3.14;
  System.out.println(d1 == d2); // true
  ```

---

### **二、引用数据类型的比较**
#### 1. **数据类型**
- 所有对象类型：`String`、`Integer`、自定义类、数组等。
- **存储的是内存地址**，变量保存的是对象的引用（内存地址）。

#### 2. **比较方式**
- **使用 `==` 比较**：比较的是对象的**内存地址**是否相同（是否指向同一个对象）。
  ```java
  String s1 = new String("Hello");
  String s2 = new String("Hello");
  System.out.println(s1 == s2); // false（地址不同）
  ```

- **使用 ==`equals()` 方法比较**==：比较对象的**内容**是否相等（需正确重写 `equals()` 方法）。
  ```java
  System.out.println(s1.equals(s2)); // true（内容相同）
  ```

#### 3. **示例**
  ```java
  Integer num1 = 100;
  Integer num2 = 100;
  System.out.println(num1 == num2); // true（缓存优化范围内，地址相同）
  
  Integer num3 = 200;
  Integer num4 = 200;
  System.out.println(num3 == num4); // false（超出缓存范围，地址不同）
  System.out.println(num3.equals(num4)); // true（值相同）
  ```

---

### **三、关键区别总结**
| **特性**         | **基本数据类型**                     | **引用数据类型**                     |
|------------------|-------------------------------------|-------------------------------------|
| **存储内容**     | 直接存储值                          | 存储对象的引用（内存地址）           |
| **比较操作**     | `==` 比较值是否相等                 | `==` 比较内存地址是否相同            |
| **内容比较**     | 无需其他方法                        | 需使用 `equals()` 方法（需正确重写） |
| **默认值**       | 有默认值（如 `int` 默认 `0`）       | 默认值为 `null`                     |
| **内存占用**     | 固定大小（如 `int` 占 4 字节）      | 对象大小不固定（依赖堆内存分配）     |

---

### **四、常见问题与注意事项**
#### 1. **字符串字面量的特殊优化**
  ```java
  String s1 = "Hello"; // 字符串常量池中的对象
  String s2 = "Hello"; // 复用常量池中的对象
  System.out.println(s1 == s2); // true（地址相同）
  ```

#### 2. **自动装箱与缓存陷阱**
  ```java
  Integer a = 127;
  Integer b = 127;
  System.out.println(a == b); // true（缓存范围 -128~127）

  Integer c = 128;
  Integer d = 128;
  System.out.println(c == d); // false（超出缓存范围）
  ```

#### 3. **数组的比较**
  ```java
  int[] arr1 = {1, 2, 3};
  int[] arr2 = {1, 2, 3};
  System.out.println(arr1 == arr2); // false（地址不同）
  System.out.println(Arrays.equals(arr1, arr2)); // true（内容相同）
  ```

#### 4. **重写 `equals()` 的规则**
  若需自定义对象的相等性比较，必须重写 `equals()` 和 `hashCode()` 方法：
  ```java
  class Person {
      private String name;
      private int age;

      @Override
      public boolean equals(Object obj) {
          if (this == obj) return true;
          if (obj == null || getClass() != obj.getClass()) return false;
          Person person = (Person) obj;
          return age == person.age && Objects.equals(name, person.name);
      }

      @Override
      public int hashCode() {
          return Objects.hash(name, age);
      }
  }
  ```

---

### **五、总结**
- **基本数据类型**：用 `==` 直接比较值。
- **引用数据类型**：
  - `==` 比较内存地址（是否为同一对象）。
  - `equals()` 比较内容是否等价（需正确实现）。
- **特殊场景**：
  - 字符串常量池优化。
  - 包装类的缓存机制（如 `Integer`）。
  - 数组内容比较需用 `Arrays.equals()`。