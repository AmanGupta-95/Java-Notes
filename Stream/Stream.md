#java 

# 🌊 Java Stream API

---

## 📌 What is Stream API?

> Stream API provides a **declarative and functional** way to process collections of data.

Instead of writing loops manually, you **stream the data** and apply **operations** like filter, map, sort, etc.

---

## 💡 Why Use Stream API?

- **Cleaner Code** ✅
    
- **Chained Operations** ✅
    
- **Parallel Processing Possible** ✅
    
- **Lazy Execution** (runs only when needed) ✅


---

## 🧪 Example 1: Filter even numbers from a list

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample1 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        numbers.stream()
               .filter(n -> n % 2 == 0) // Keep only even numbers
               .forEach(System.out::println); // Print them
    }
}
```

🖥️ Output:
```
2
4
6
```

---

## 🧪 Example 2: Map to square of numbers

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample2 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3);

        numbers.stream()
               .map(n -> n * n) // Square each number
               .forEach(System.out::println);
    }
}
```

🖥️ Output:
```
1
4
9
```

---

## 🧪 Example 3: Count words starting with “a”

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample3 {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "avocado", "grape");

        long count = words.stream()
                          .filter(w -> w.startsWith("a"))
                          .count();

        System.out.println("Words starting with 'a': " + count);
    }
}
```

🖥️ Output:
```
Words starting with 'a': 2
```

---

## 🔗 Common Stream Operations

|Operation|Description|
|---|---|
|`filter()`|Keep elements that match condition|
|`map()`|Transform each element|
|`sorted()`|Sort stream|
|`forEach()`|Terminal operation for printing/logic|
|`collect()`|Convert back to list, set, etc.|
|`count()`|Count elements|
|`distinct()`|Remove duplicates|
|`limit(n)`|Keep only first n elements|

---

## 🧰 Example 4: Collect to List

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample4 {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ram", "Shyam", "Ravi", "Ritika");

        List<String> result = names.stream()
                                   .filter(n -> n.startsWith("R"))
                                   .collect(Collectors.toList());

        System.out.println(result);
    }
}
```

🖥️ Output:
```
[Ram, Ravi, Ritika]
```

## ⚠️ Important Notes

- **Streams don’t change the original data**
    
- Stream operations are **lazy** — they don’t execute until a terminal operation is called (`forEach`, `collect`, `count`, etc.)
