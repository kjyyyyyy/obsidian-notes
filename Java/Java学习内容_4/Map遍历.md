太棒了👏！你已经进入 Java 集合的进阶阶段，现在我们要学习 **Map 的三种常见遍历方式**：

1. **通过 `entrySet()` 遍历键值对（Key-Value）**
2. **通过 `keySet()` 遍历所有键（Key）**
3. **使用 Lambda 表达式 + `forEach()` 遍历**

下面我会用最清晰、最适合新手的方式一个一个讲解。

---

## 🧠 一、准备工作：创建一个 Map 示例

我们先准备一个简单的 `HashMap`：

```java
import java.util.HashMap;
import java.util.Map;

public class MapTraverseDemo {
    public static void main(String[] args) {
        Map<String, Integer> scores = new HashMap<>();
        scores.put("Alice", 90);
        scores.put("Bob", 85);
        scores.put("Charlie", 95);
        
        // 下面我们将用三种方式遍历这个 Map
    }
}
```

---

## 🔁 二、第一种：通过 `entrySet()` 遍历键值对（推荐）

这是最常用的一种方式，可以同时拿到 Key 和 Value。

### ✅ 使用增强型 for 循环（适合初学者）

```java
for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    String key = entry.getKey();
    Integer value = entry.getValue();
    System.out.println("姓名: " + key + ", 分数: " + value);
}
```

### ✅ 输出结果：
```
姓名: Alice, 分数: 90
姓名: Bob, 分数: 85
姓名: Charlie, 分数: 95
```

📌 这是**最推荐的遍历方式**，因为你一次就能拿到 Key 和 Value。

---

## 🔁 三、第二种：通过 `keySet()` 遍历所有键（Key）

这种方式只遍历所有的 Key，然后通过 Key 获取对应的 Value。

### ✅ 示例代码：

```java
for (String name : scores.keySet()) {
    int score = scores.get(name);
    System.out.println("姓名: " + name + ", 分数: " + score);
}
```

📌 优点：只关心 Key 时可以用。  
⚠️ 缺点：每次都要调用 `get()`，效率略低。

---

## 🔁 四、第三种：使用 Lambda 表达式 + `forEach()` 遍历（简洁现代写法）

Java 8 引入了 `forEach(BiConsumer)` 方法，支持 Lambda 表达式，非常简洁！

### ✅ 示例代码：

```java
scores.forEach((name, score) -> {
    System.out.println("姓名: " + name + ", 分数: " + score);
});
```

### ✅ 简洁版（一行写法）：

```java
scores.forEach((k, v) -> System.out.println(k + ": " + v));
```

📌 这是目前最推荐的“现代风格”写法，简单又优雅！

---

## 📝 五、总结对比表

| 遍历方式 | 是否能获取 Key | 是否能获取 Value | 推荐程度 | 适用场景 |
|----------|----------------|------------------|-----------|------------|
| `entrySet()` | ✅ 是 | ✅ 是 | ⭐⭐⭐⭐⭐ | 最常用，推荐 |
| `keySet()`   | ✅ 是 | ✅ 是（需 get） | ⭐⭐⭐ | 只关注 Key 或旧版本 Java |
| `forEach()` + Lambda | ✅ 是 | ✅ 是 | ⭐⭐⭐⭐⭐ | Java 8+ 推荐写法 |

---

## 🧩 六、拓展知识（可选）

### 1️⃣ 如何按 Value 排序？

如果你想按分数排序输出，可以这样写：

```java
scores.entrySet()
      .stream()
      .sorted(Map.Entry.comparingByValue())
      .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
```

---

### 2️⃣ 自定义对象作为 Key 的注意事项

如果你用自定义类（如 `Person`）作为 Key，记得要重写：

- `equals()` 方法
- `hashCode()` 方法

否则可能会出现：

```java
map.get(person1) != map.get(person2) // 即使两个 person 内容一样
```

---

## ✅ 七、一句话总结

> **Map 的三种常见遍历方式分别是：**
> 1. 通过 `entrySet()` 同时获取 Key 和 Value（推荐）
> 2. 通过 `keySet()` 遍历 Key，再 `get()` 获取 Value
> 3. 使用 Lambda 表达式 `forEach((k, v) -> {})`（现代简洁写法）

---

如果你希望我帮你整理一份 **“Map 常见 API 和遍历方式速查表”**，或者想看更多实战案例（比如统计词频、合并 Map 等），也可以告诉我 😊 我很乐意继续陪你一起学下去！

继续加油，Java 学习越来越熟练啦！🚀