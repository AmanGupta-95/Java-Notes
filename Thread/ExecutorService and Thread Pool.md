#java 

# ⚙️ `ExecutorService` & Thread Pool in Java

---

## ❓ Why Not Just `new Thread()`?

- ❌ Creating a new thread for every task is **expensive**.
    
- ❌ No control over number of threads.
    
- ❌ Can cause **memory issues** if tasks keep growing.

✅ Use a **Thread Pool** — reuse threads instead of creating new ones!

---

## ✅ What is `ExecutorService`?

> `ExecutorService` is part of `java.util.concurrent`  
> It **manages a pool of threads** and allows you to submit tasks for asynchronous execution.

---

## 🔧 Basic Usage

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        Runnable task = () -> {
            System.out.println("Running in thread: " + Thread.currentThread().getName());
        };

        executor.submit(task); // Submit 1 task
        executor.shutdown();   // Important! Shut down after tasks finish
    }
}
```

---

## 🧰 Common Factory Methods

|Method|Description|
|---|---|
|`Executors.newFixedThreadPool(n)`|Fixed number of threads|
|`Executors.newCachedThreadPool()`|Grows as needed, reuses idle threads|
|`Executors.newSingleThreadExecutor()`|One thread only (like a queue)|
|`Executors.newScheduledThreadPool(n)`|For delayed/repeating tasks|

---

## 🔁 Example: Multiple Tasks with Thread Pool

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

for (int i = 1; i <= 5; i++) {
    int taskId = i;
    executor.submit(() -> {
        System.out.println("Task " + taskId + " running in " + Thread.currentThread().getName());
    });
}

executor.shutdown(); // No more tasks allowed
```

## 🔄 Difference: `submit()` vs `execute()`

|Method|Returns|Usage|
|---|---|---|
|`submit()`|`Future<?>`|Allows result tracking|
|`execute()`|void|Fire-and-forget|

---

## 🔮 What is `Future`?

A `Future` represents the **result of an asynchronous computation**.

```java
Future<Integer> future = executor.submit(() -> {
    return 10 + 20;
});

Integer result = future.get(); // Blocks until result is available
```

---
## 🛑 Always Shutdown the Executor

```java
executor.shutdown();              // Graceful shutdown
executor.awaitTermination(10, TimeUnit.SECONDS); // Optional
executor.shutdownNow();           // Force stop (risky)
```

---

## 🧠 Real-World Use Cases

- 🔄 Sending emails in background
    
- 📦 Processing queues
    
- 📈 Scheduling reports
    
- ⚙️ Spring Boot async controllers (`@Async` internally uses `Executor`)

