#java 

# 🔄 Java Thread Lifecycle

---

## 🧠 What is Thread Lifecycle?

A thread in Java goes through **multiple states** during its lifetime. Java defines these states in the `Thread.State` enum.

---

## 📊 Lifecycle Stages

```
stateDiagram-v2
    [*] --> NEW
    NEW --> RUNNABLE: start()
    RUNNABLE --> RUNNING: picked by scheduler
    RUNNING --> WAITING: wait()/join()
    RUNNING --> TIMED_WAITING: sleep(), join(time)
    RUNNING --> BLOCKED: trying to access locked resource
    WAITING --> RUNNABLE: notify()
    TIMED_WAITING --> RUNNABLE: time expires
    BLOCKED --> RUNNABLE: lock released
    RUNNING --> TERMINATED: completed or exception
    [*] --> TERMINATED
```

---

## 📝 Lifecycle Stages Explained

### 1. **NEW**

Thread is created but not yet started.

```java
Thread t = new Thread(); // NEW
```

---

### 2. **RUNNABLE**

Thread is **ready to run**, but waiting for CPU time.

```java
t.start(); // moves to RUNNABLE
```

---

### 3. **RUNNING**

Thread is **actually executing** code (chosen by the CPU scheduler).

➡️ You don't control this directly — the OS does.

---

### 4. **BLOCKED**

Thread is **waiting to access a locked resource** (e.g., synchronized block held by another thread).

---

### 5. **WAITING**

Thread is **waiting indefinitely** for another thread to notify it (e.g., `wait()`, `join()`).

```java
t.join(); // waits for t to finish
```

### 6. **TIMED_WAITING**

Thread waits for **a specified amount of time**.

```java
Thread.sleep(1000);        // 1 second
t.join(2000);              // wait max 2 seconds
```

### 7. **TERMINATED**

Thread is **finished** — either completed successfully or due to an exception.

---

## 🧪 Example: Sleep and Join

```java
public class MyThread extends Thread {
    public void run() {
        System.out.println("Running: " + Thread.currentThread().getName());
        try {
            Thread.sleep(2000); // TIMED_WAITING
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Finished: " + Thread.currentThread().getName());
    }
}

Thread t1 = new MyThread();
t1.start();                // RUNNABLE → RUNNING
t1.join();                 // WAITING in main thread
System.out.println("Main thread resumes");
```

---

## ✅ Summary Table

| State           | Trigger                                  |
| --------------- | ---------------------------------------- |
| `NEW`           | Thread created                           |
| `RUNNABLE`      | `.start()` called                        |
| `RUNNING`       | Chosen by CPU scheduler                  |
| `BLOCKED`       | Waiting for lock                         |
| `WAITING`       | `.wait()` or `.join()` (no timeout)      |
| `TIMED_WAITING` | `.sleep()`, `.join(time)`, `.wait(time)` |
| `TERMINATED`    | Thread ends normally or by exception     |
