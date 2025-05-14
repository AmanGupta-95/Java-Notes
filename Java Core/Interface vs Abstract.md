#java 

## 🧠 Is Interface Better Than Abstract Class?

---
# 🧠 TL;DR

> 🎯 **Use Interface** for contracts (multiple abilities like `Flyable`, `Swimmable`).  
> 🏛️ **Use Abstract Class** when you have some common code to share among related classes.

---

# 1. Interface: 💬 "What should be done?"

---

- Defines a **contract**.
- No implementation (only method signatures).
- A class **implements** an interface.
- **Multiple interfaces** can be implemented by a single class (Java supports multiple interfaces, not multiple class inheritance).

---

### Example:

```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

public class Duck implements Flyable, Swimmable {
    public void fly() {
        System.out.println("Duck flies");
    }
    
    public void swim() {
        System.out.println("Duck swims");
    }
}
```
✅ **Focus**: "What should the object do?" (Not how)

---

# 2. Abstract Class: 🛠️ "What it partially is"

---

- Can have **both** abstract methods (no body) **and** concrete methods (with body).
- A class **extends** an abstract class.
- You can have **fields**, **constructors**, and **non-abstract methods**.
- **Single inheritance only** (a class can extend only one abstract class).

---

### Example:

```java
abstract class Animal {
    String name;

    public Animal(String name) {
        this.name = name;
    }

    public void sleep() {
        System.out.println(name + " sleeps");
    }

    abstract void makeSound();
}

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    public void makeSound() {
        System.out.println(name + " barks");
    }
}
```
✅ **Focus**: "What the object partly _is_ and partly _does_."

---

# 📌 So, which one is better?

|Criteria|Interface|Abstract Class|
|---|---|---|
|Purpose|100% abstraction (what to do)|Partial abstraction (what + how)|
|Methods|Only method signatures (Java 8+ allows `default` methods)|Can have both abstract and normal methods|
|Multiple inheritance support|Yes, multiple interfaces|No, only single abstract class|
|Variables|`public static final` only|Can have normal instance variables|
|Constructor support|❌ No constructors|✅ Yes, can have constructors|

---

# 🚀 Best Practice:

|Situation|What to Use|
|---|---|
|Only define capabilities/behavior|✅ Interface|
|Share common code among subclasses|✅ Abstract Class|
