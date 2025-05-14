#java #static
## 🧠 Where is `static` stored in Java memory?
---

### 📌 TL;DR

> 🔹 **Static = Method Area**  
> 🔹 **Object = Heap**  
> 🔹 **Local Variables = Stack**


### 🔹 Java Memory Areas (Simplified)

|Memory Area|Stores|
|---|---|
|**Heap**|Objects and their instance variables|
|**Stack**|Method calls, local variables (per thread)|
|**Method Area** (or **MetaSpace** in Java 8+)|Class metadata, static variables, static methods|

---

### 🔸 So where does `static` go?

|Static Thing|Stored In|Why?|
|---|---|---|
|`static` variable|✅ **Method Area**|Belongs to class, not object|
|`static` method|✅ **Method Area**|Loaded with class, reused globally|
|`static` block|✅ **Method Area**|Runs once when class loads|

---

### ✅ Example

```java
public class MyClass {
    static int count = 0; // Stored in method area

    static {
        System.out.println("Static block runs once");
    }

    static void greet() {
        System.out.println("Hello from static method");
    }

    public void sayHi() {
        int x = 10; // Stored in stack (local variable)
        System.out.println("Hi");
    }
}
```

### 🔹 Key Notes

- `static` is **shared** across all objects.
    
- Memory for static things is allocated **when the class is loaded**, not when objects are created.
    
- Local variables and method calls are stored on the **stack**.
    
- Object data (non-static) is stored on the **heap**.