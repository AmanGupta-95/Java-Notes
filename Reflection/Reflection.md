#java 

## 🧠 What is Reflection in Java?

---
# 📌 TL;DR:

|Aspect|Summary|
|---|---|
|What?|Inspect/modify program structure at runtime|
|Useful for?|Frameworks, dynamic libraries, custom processors|
|Risks?|Slower, less safe than normal code|

---
### 🔹 Simple Definition

> 🪞 **Reflection is the ability of a Java program to inspect and modify its own structure (classes, methods, fields, constructors) at runtime.**

✅ You can access and manipulate **classes**, **objects**, **fields**, **methods**, and **constructors** **dynamically** without knowing their names at compile time.

---

## 🎯 Why Use Reflection?

- **Frameworks** (like Spring, Hibernate) use it internally for Dependency Injection, ORM, AOP, etc.
- To **build libraries** that work on unknown classes.
- To create **dynamic code** (example: plugins, generic libraries).
- To implement **[[Custom Annotation]] Processor**.

---

# 🛠️ Basic Example of Reflection

```java
import java.lang.reflect.Method;

public class ReflectionExample {
    public static void main(String[] args) throws Exception {
        // Get Class object
        Class<?> clazz = Class.forName("Car");

        // Create instance
        Object carObj = clazz.getDeclaredConstructor().newInstance();

        // Get method and invoke it
        Method method = clazz.getMethod("drive");
        method.invoke(carObj);
    }
}

class Car {
    public void drive() {
        System.out.println("Car is driving...");
    }
}
```

✅ Output:

```
Car is driving...
```

---

# 🔥 Important Reflection Classes

|Class|Purpose|
|---|---|
|`Class`|Represents a class or interface|
|`Method`|Represents methods|
|`Field`|Represents fields (variables)|
|`Constructor`|Represents constructors|

---

# 📚 How to Use Reflection (Common Operations)

---

1. Get `Class` Object

```java
Class<?> clazz = Class.forName("com.example.MyClass"); 
// or
MyClass obj = new MyClass();
Class<?> clazz2 = obj.getClass();
```

2. Create Object Dynamically

```java
Object obj = clazz.getDeclaredConstructor().newInstance();
```

3. Access Fields (Variables)

```java
Field field = clazz.getDeclaredField("someField");
field.setAccessible(true); // Bypass private
field.set(obj, "New Value"); // Set value
Object value = field.get(obj); // Get value
```

4. Access Methods

```java
Method method = clazz.getMethod("someMethod");
method.invoke(obj); // Call method
```

5. Access Constructors

```java
Constructor<?> constructor = clazz.getConstructor(String.class);
Object obj = constructor.newInstance("ParamValue");
```

---
# 🚨 Important: Reflection comes with some Risks!

| Risk               | Explanation                                         |
| ------------------ | --------------------------------------------------- |
| Slower Performance | Reflection is slower because it uses extra steps    |
| Security Risk      | You can access private data (violate encapsulation) |
| More Error-prone   | No compile-time checking (errors only at runtime)   |

---
# 🌟 Bonus: Real Usage of Reflection in Spring Boot

- **Dependency Injection**:  
    `@Autowired` fields are injected using Reflection.
- **Entity Mapping**:  
    Hibernate maps Java fields to Database columns using Reflection.
- **AOP (Aspect-Oriented Programming)**:  
    Methods are intercepted and modified at runtime.