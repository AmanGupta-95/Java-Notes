#java 

## 🧠 Java Memory Model — Stack vs Heap vs Method Area

### 📌 TL;DR

> 🧠 **Method Area** holds class structure and static stuff.  
> 💾 **Heap** stores objects (via `new`).  
> ⚡ **Stack** is for method calls and temporary values.


Java uses different memory areas to manage your program efficiently. Each has a **specific purpose**.

---

### 🔸 1. **Stack Memory**

> ⚙️ Per thread, fast, temporary

- Stores:
    
    - Method calls
        
    - Local variables
        
    - Function parameters
        
- Memory is **freed automatically** when a method ends.
    
- Each thread has its **own stack**.

```java
void show() {
    int x = 5; // stored in stack
}
```

### 🔸 2. **Heap Memory**

> 🧱 Shared, for objects and instances

- Stores:
    
    - All objects created using `new`
        
    - Instance variables (non-static fields)
        
- Shared by **all threads**
    
- Managed by the **Garbage Collector**

```java
class Dog {
    String name; // Stored in heap
}
Dog d = new Dog(); // Object goes to heap

```

### 3. **Method Area (a.k.a Class Area or MetaSpace)**

> 📦 Shared, stores class-level data

- Stores:
    
    - **Class bytecode**
        
    - **Static variables**
        
    - **Static methods**
        
    - **Method definitions**
        
    - **Constant pool**
        
- Exists **once per JVM**.
    
- Data loaded here stays until the class is unloaded.

```java
class Cat {
    static int legs = 4; // Stored in method area
    static void speak() { } // Also in method area
}
```

### 🧾 Comparison Table

|Feature|Stack|Heap|Method Area|
|---|---|---|---|
|Stores|Local vars, calls|Objects|Class-level stuff|
|Lifetime|Per method call|Until GC|Until class unload|
|Shared?|❌ No (per thread)|✅ Yes|✅ Yes|
|Speed|⚡ Fast|🐢 Slower|⚖️ Balanced|
|Garbage Collected?|❌ No|✅ Yes|✅ Yes|