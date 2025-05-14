#java 

## 🔹 What is a Lambda Function in Java?

A **lambda function** is a **short way to write a method** (usually for interfaces with one method, called _functional interfaces_).  
It lets you write **cleaner, more concise code**, especially when working with collections, streams, etc.

🧠 Syntax

```java
(parameters) -> { method body }
```

🔸 Functional Interface Example

```java
@FunctionalInterface
interface Greetable {
    void greet(String name);
}
```

✅ Using Lambda

```java
Greetable g = (name) -> {
    System.out.println("Hello, " + name);
};

g.greet("John");
```

Output: `Hello, John`

🔹 Without Lambda (Traditional Way)

```java
Greetable g = new Greetable() {
    public void greet(String name) {
        System.out.println("Hello, " + name);
    }
};
```

Lambda makes the same thing shorter and easier to read ✅

### 🔸 More Examples

1. No Parameters

```java
Runnable r = () -> {
    System.out.println("Running...");
};
r.run();
```

2. With Parameters and Return Value

```java
interface Adder {
    int add(int a, int b);
}

Adder sum = (a, b) -> a + b;
System.out.println(sum.add(5, 3)); // Output: 8
```

### 🔹 Where It's Commonly Used

- `Streams`
    
- `Collections` (like `List.forEach`)
    
- `Runnable`, `Comparator`, etc.
    
- Spring's functional APIs

### ✅ Summary

- Lambda = anonymous function (no name)
    
- Used with **functional interfaces** (one abstract method)
    
- Clean, short, and readable code