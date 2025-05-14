#java 

# 🧱 What is a POJO in Java?

---

## 🔹 POJO = **Plain Old Java Object**

> A POJO is a simple Java class that **does not depend on any framework, inheritance, or annotations** — it's just used to **store data**.

---

## ✅ Features of a POJO

- No need to extend any class
    
- No need to implement any interface
    
- Typically contains:
    
    - `private` fields (variables)
        
    - `public` getters/setters
        
    - A no-arg constructor
        
    - `toString()`, `equals()`, `hashCode()` (optional but useful)

---

## 🧾 Example: POJO Class

```java
public class Person {
    private String name;
    private int age;

    // Constructor
    public Person() {}

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters
    public String getName() { return name; }
    public int getAge() { return age; }

    // Setters
    public void setName(String name) { this.name = name; }
    public void setAge(int age) { this.age = age; }

    @Override
    public String toString() {
        return name + " is " + age + " years old.";
    }
}
```

---

## 🔍 Where are POJOs used?

- Data Transfer Objects (DTOs)
    
- JSON/XML serialization (e.g., with Jackson in Spring Boot)
    
- Hibernate/JPA entities
    
- Form inputs in APIs

---

## 🧠 Why use POJOs?

- Simplicity and readability
    
- Easy to convert to/from JSON/XML
    
- Used as **input/output** objects in REST APIs
    
- Compatible with most frameworks (Spring, Hibernate, etc.)