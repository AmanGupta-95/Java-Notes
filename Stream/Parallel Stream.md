#java 

# 🧵 Parallel Streams in Java

---

## 📌 What is a Parallel Stream?

> A **parallel stream** divides the data into multiple parts and processes them **concurrently** using **multiple threads** (in contrast to the sequential stream which uses a single thread).

---

## ⚙️ Syntax

Just call `.parallelStream()` instead of `.stream()`:
```java
list.parallelStream()
```

🧪 Example 1: Simple Parallel Stream

```java
import java.util.Arrays;
import java.util.List;

public class ParallelExample1 {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ram", "Shyam", "Mohan", "Ravi", "Radha");

        names.parallelStream()
             .forEach(name -> {
                 System.out.println(name + " - " + Thread.currentThread().getName());
             });
    }
}
```

🖥️ Output (thread names will vary):
```
Ram - ForkJoinPool.commonPool-worker-3
Ravi - ForkJoinPool.commonPool-worker-5
Mohan - ForkJoinPool.commonPool-worker-7
Shyam - main
Radha - ForkJoinPool.commonPool-worker-2
```

✅ You can see multiple threads being used!

🧪 Example 2: Compare time between `stream()` vs `parallelStream()`

```java
import java.util.List;
import java.util.stream.IntStream;
import java.util.stream.Collectors;

public class ParallelExample2 {
    public static void main(String[] args) {
        List<Integer> numbers = IntStream.rangeClosed(1, 1000000)
                                         .boxed()
                                         .collect(Collectors.toList());

        long start = System.currentTimeMillis();
        long count = numbers.stream()
                            .filter(n -> n % 2 == 0)
                            .count();
        long end = System.currentTimeMillis();
        System.out.println("Sequential time: " + (end - start) + "ms");

        start = System.currentTimeMillis();
        count = numbers.parallelStream()
                       .filter(n -> n % 2 == 0)
                       .count();
        end = System.currentTimeMillis();
        System.out.println("Parallel time: " + (end - start) + "ms");
    }
}
```

🖥️ Output (will vary depending on your system):
```
Sequential time: 45ms
Parallel time: 16ms
```

---

## ⚠️ When **Not** to Use Parallel Streams

|❌ Don’t use parallelStream if...|Why?|
|---|---|
|Working with I/O (like files or DB)|Parallelism may cause contention|
|The data size is small|Overhead of threading > benefit|
|The operations are **not thread-safe**|May result in inconsistent behavior|
|You need to preserve **order of processing**|Order is not guaranteed in parallel stream|

---

## ✅ Good Use Cases

- Large data processing
    
- CPU-intensive calculations
    
- Independent operations (no shared state)
