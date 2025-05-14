#java 

## 📘 Interface vs Class in Java

---

### 🔹 What is a `class`?

A `class` is a blueprint for creating **objects**. It can have:

- **Variables (fields)**
- **Methods (with implementation)**
- **Constructors**

```java
public class Animal {     
	String name;      
	public void speak() {         
	System.out.println("Animal speaks");     
	} 
}
```


✅ You can create an object from a class:

```java
Animal a = new Animal(); a.speak();
```

---

### 🔸 What is an `interface`?

An `interface` is like a **contract**. It **only declares methods** (no implementation, until Java 8+).

```java
public interface Flyable {     
	void fly(); // No body
}
```

✅ A class **implements** an interface:

```java
public class Bird implements Flyable {     
	public void fly() {         
		System.out.println("Bird is flying");     
	}
}
```

---

### 🆚 Differences: Interface vs Class

|Feature|Class|Interface|
|---|---|---|
|Has fields|✅ Yes|⚠️ Only `public static final` constants|
|Has method body|✅ Yes|❌ No (only from Java 8+: `default`/`static` methods allowed)|
|Instantiable|✅ Yes (`new`)|❌ No|
|Inheritance type|`extends`|`implements`|
|Multiple inheritance|❌ No (single class only)|✅ Yes (can implement multiple interfaces)|
|Constructor allowed|✅ Yes|❌ No constructor|

---

### 🧠 Use Case Summary

- Use a **class** when:
    
    - You want to define data + behavior (real objects).
        
- Use an **interface** when:
    
    - You want to define capabilities like `Flyable`, `Drivable`, etc.
        
    - You need **multiple inheritance of behavior**.
        

---

### ✅ Example: Interface + Class

```java
interface Printable {
    void print();
}

class Document implements Printable {
    public void print() {
        System.out.println("Printing document...");
    }
}
```