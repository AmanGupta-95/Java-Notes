#OOPS #java 

## 🧠 Basics of OOPS in Java

OOPS is based on **4 main principles**:

---

# 📌 TL;DR: 4 Pillars of OOPS

| Principle     | Meaning                         | Example                          |
| ------------- | ------------------------------- | -------------------------------- |
| Encapsulation | Hide internal data              | Private fields + getters/setters |
| Inheritance   | Child inherits parent           | `class Dog extends Animal`       |
| Polymorphism  | Many forms (overload/override)  | `sound()` method changes         |
| Abstraction   | Hide complexity, show essential | Abstract classes/interfaces      |

---
# 1. Encapsulation (Data Hiding)

---

> **Binding** data (variables) and code (methods) together and **restricting direct access**.

✅ Achieved by:

- Making fields `private`
- Providing `public` getters/setters

---

### Example:

```java
public class Person {
    private String name; // Hidden from outside
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        if (!name.isEmpty()) {
            this.name = name;
        }
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }
}
```
**Why?**  
🔒 Prevents invalid or harmful changes to the object.

---

# 2. Inheritance (Is-a relationship)

---

> **One class (child) inherits properties and behaviors** of another class (parent).

✅ Achieved by using `extends` keyword.

---

### Example:

```java
public class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("The dog barks.");
    }
}
```

```java
Dog d = new Dog();
d.eat();  // inherited from Animal
d.bark(); // own method
```

**Why?**  
🧩 Reusability and code organization.

---

# 3. Polymorphism (Many Forms)

---

> Ability of an object to **take many forms**.

Two types:

- **Compile-Time (Method Overloading)**
- **Run-Time (Method Overriding)**

---

### ✨ Compile-Time Polymorphism (Method Overloading)

Same method name, different parameters.
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

### ✨ Run-Time Polymorphism (Method Overriding)

Child class provides its **own version** of a parent method.

```java
public class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

public class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("Cat meows");
    }
}
```

```java
Animal myCat = new Cat();
myCat.sound(); // Output: Cat meows
```

**Why?**  
🎭 Flexibility and dynamic behavior at runtime.

---

# 4. Abstraction (Hiding Complexity)

---

> **Showing only essential features** and **hiding complex details**.

✅ Achieved by:

- **Abstract Classes** (`abstract` keyword)
- **Interfaces**

---

### Example:

```java
abstract class Vehicle {
    abstract void start();
}

public class Car extends Vehicle {
    @Override
    public void start() {
        System.out.println("Car starts with a key.");
    }
}
```

```java
Vehicle v = new Car();
v.start(); // "Car starts with a key."
```
**Why?**  
🕵️‍♂️ Focuses on **what an object does**, not **how it does** it.
