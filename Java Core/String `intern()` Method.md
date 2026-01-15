
#java

## 📌 What is `intern()`

`intern()` is a method of the `String` class that **adds the string to the String Constant Pool (SCP)** and returns the **reference from the pool**.

> If the string already exists in the pool, it returns the existing reference.

---
## 📦 Package

`java.lang.String`

---

## 🔹 Method Signature

`public native String intern();`

---

## 🧠 How String Pool Works

- **String literals** are stored in the **String Constant Pool**
    
- `new String()` creates objects in **Heap memory**
    
- `intern()` ensures **only one copy** of a string exists in the pool
    

---

## 🔁 Behavior Flow

1. JVM checks **String Pool**
    
2. If string exists → return pooled reference
    
3. If not exists → add to pool and return reference
    

---

## 🔹 Example 1: Literal vs `new String()`

```java
String s1 = "java";
String s2 = new String("java");

System.out.println(s1 == s2); // false
```

Reason:
- `s1` → SCP
- `s2` → Heap

---

## 🔹 Example 2: Using `intern()`

```java
String s1 = "java";
String s2 = new String("java").intern();

System.out.println(s1 == s2); // true
```

Now both point to **same SCP object**

---

## 🔹 Example 3: Two Heap Strings

```java
String s1 = new String("spring");
String s2 = new String("spring");

System.out.println(s1 == s2); // false

s1 = s1.intern();
s2 = s2.intern();

System.out.println(s1 == s2); // true
```

---

## 🧠 Java Version Behavior

### 🔸 Before Java 7

- String Pool stored in **PermGen**
    
- Interned strings copied from Heap → PermGen
    

### 🔸 Java 7+

- String Pool moved to **Heap**
    
- `intern()` stores **reference**, not copy
    

> This reduced `OutOfMemoryError: PermGen space`

---

## 🧪 Memory Visualization

```js
Heap
 ├── new String("java")
 └── String Pool
       └── "java"
```

After `intern()` → both references point to `"java"` in pool

---

## ⚠️ Important Notes

- `intern()` **saves memory** only when many duplicate strings exist
    
- Excessive use may **increase GC pressure**
    
- Avoid in hot paths unless profiling proves benefit
    

---

## ⚔️ `==` vs `equals()` with `intern()`

```java
String a = new String("hello").intern();
String b = "hello";

a == b        // true
a.equals(b)  // true
```

## 📌 When to Use `intern()`

✅ Good use cases:

- Large number of **duplicate strings**
    
- Memory-sensitive applications
    
- Framework-level optimizations

❌ Avoid when:

- Strings are mostly unique
    
- Performance-critical loops