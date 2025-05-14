#java 

# 🧵 Java Threads – Basics of Multithreading

---

## 🧠 What is a Thread?

> A **Thread** is the smallest unit of execution in a program.  
> Java allows multiple threads to run **concurrently** — even in the same application.

### 🟢 Main Thread

Every Java app starts with **one main thread**:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Main thread: " + Thread.currentThread().getName());
    }
}
```

---

## 🔧 Ways to Create a Thread

### 1. **Extending `Thread` class**

```java
public class MyThread extends Thread {
    public void run() {
        System.out.println("Running in " + Thread.currentThread().getName());
    }
}

// Usage
MyThread t1 = new MyThread();
t1.start(); // start() → creates new thread, run() is called internally
```

---

### 2. **Implementing `Runnable` interface**

```java
public class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Running with Runnable");
    }
}

// Usage
Thread t2 = new Thread(new MyRunnable());
t2.start();
```

✅ **Runnable is preferred** over extending Thread (as Java supports only single inheritance).

---

### 3. **Using Lambda (short version)**

```java
Thread t3 = new Thread(() -> {
    System.out.println("Running with Lambda!");
});
t3.start();
```

---

## 🕹️ Important Thread Methods

|Method|Description|
|---|---|
|`start()`|Starts a new thread|
|`run()`|Logic to run in the thread|
|`sleep(ms)`|Pause thread for milliseconds|
|`join()`|Waits for thread to finish|
|`isAlive()`|Checks if thread is still running|
|`setName()`|Sets thread name|

---

## 🧪 Example: Multiple Threads

```java
public class MyTask implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread: " + Thread.currentThread().getName() + " → " + i);
        }
    }
}

// Usage
Thread t1 = new Thread(new MyTask());
Thread t2 = new Thread(new MyTask());

t1.start();
t2.start();
```

---

## 🚫 Common Mistakes

- ❌ Calling `run()` directly instead of `start()` → runs on main thread, not new one.
- ❌ Not handling `InterruptedException` when using `sleep()` or `join()`.

---

## 🧠 Summary

- Use `Runnable` or lambda for cleaner code.
- `start()` → starts a **new thread**
- Java thread handling is **low-level**, for advanced control use `ExecutorService`.