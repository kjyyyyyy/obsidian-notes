在 Java 中，`this` 是一个特殊的关键字，表示**当前对象的引用**。它在类中的主要用途如下：

---

### **1. 区分成员变量和局部变量**
当成员变量（类的属性）和局部变量（如方法参数或方法内变量）**同名**时，可以用 `this` 明确指定访问的是成员变量。

#### **示例：构造方法中的 `this`**
```java
public class Student {
    private String name; // 成员变量

    // 构造方法参数 name 与成员变量同名
    public Student(String name) {
        this.name = name; // 用 this.name 表示成员变量，右边的 name 是参数
    }
}
```

#### **示例：Setter 方法中的 `this`**
```java
public void setName(String name) {
    this.name = name; // 明确将参数 name 赋值给成员变量 name
}
```

---

### **2. 调用当前类的其他构造方法**
在构造方法中，可以用 `this()` 调用本类的其他构造方法，但必须放在构造方法的**第一行**。

#### **示例：构造方法重载**
```java
public class Student {
    private String name;
    private int age;

    // 无参构造方法
    public Student() {
        this("默认姓名", 18); // 调用有参构造方法
    }

    // 有参构造方法
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

### **3. 作为当前对象的引用**
`this` 可以表示当前对象本身，用于：
- 将对象自身作为参数传递给其他方法。
- 在方法中返回当前对象（链式调用）。

#### **示例：传递对象自身**
```java
public class Student {
    public void printInfo() {
        System.out.println("学生信息：" + this); // 隐式调用 toString()
    }

    public void registerToCourse(Course course) {
        course.addStudent(this); // 将当前学生对象传递给课程类的方法
    }
}
```

---

### **4. 解决内部类访问外部类成员的问题**
在内部类中，若需要访问外部类的成员，可以用 `外部类名.this.成员`。

#### **示例：内部类中使用 `this`**
```java
public class Outer {
    private int value = 10;

    class Inner {
        public void printValue() {
            System.out.println("外部类的 value: " + Outer.this.value); // 访问外部类成员
        }
    }
}
```

---

### **注意事项**
1. **`this` 不能在静态方法中使用**  
   静态方法属于类，而非对象，因此无法使用 `this`。
   ```java
   public static void staticMethod() {
       // this.name = "Tom"; // 错误！静态方法中不能使用 this
   }
   ```

2. **`this()` 必须放在构造方法的首行**  
   若同时调用 `this()` 和 `super()`，会导致编译错误。

---

### **总结**
- **核心作用**：明确指向当前对象的成员变量或方法。
- **典型场景**：
  - 变量名冲突时区分成员变量和局部变量。
  - 构造方法的重载调用。
  - 链式方法设计（返回 `this`）。
- **关键限制**：无法在静态上下文中使用。