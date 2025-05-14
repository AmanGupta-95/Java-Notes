#java 

## 🧠 Why Use Getters and Setters Instead of Direct Variable Access?

---

### 📌 TL;DR

> 🔒 **Getters and Setters = Controlled Access**  
> 🚫 **Direct Public Fields = No Rules, High Risk**

### 🔸 Problem with Direct Variable Access

When you make variables `public`, anyone can:

- Change them **freely**, without rules
    
- Set **invalid values**
    
- Bypass **security checks**
    
- Make debugging and maintenance **very hard**
    

---

### 🔹 Real Scenarios: When Direct Access is Dangerous

---

### 1. **Invalid Data Entry**

```java
public class User {
    public int age;
}

// Somewhere else
User u = new User();
u.age = -5; // 🚨 Invalid age!
```

**Problem**: No one should have age `-5`, but direct access allows it.

✅ Using setter:

```java
public void setAge(int age) {
    if (age > 0) {
        this.age = age;
    } else {
        throw new IllegalArgumentException("Age must be positive");
    }
}
```

### 2. **Security Breach**

Imagine a banking app:

```java
public class BankAccount {
    public double balance;
}
```

```java
BankAccount b = new BankAccount();
b.balance = 1000000; // 🚨 Hackers can modify balance easily!
```

✅ Better with private + controlled setter:

```java
private double balance;

public void deposit(double amount) {
    if (amount > 0) balance += amount;
}

public void withdraw(double amount) {
    if (amount > 0 && amount <= balance) balance -= amount;
    else throw new IllegalArgumentException("Invalid withdrawal");
}
```

Now no one can **directly change** the balance!

### 3. **Future Changes Without Breaking Code**

If you use getters/setters, you can **change the internal logic later** without breaking other parts of your app.

Example:

```java
public String getName() {
    return name.toUpperCase();
}
```

You can now control **how** data is presented.

If you used public fields, you'd have to change code **everywhere**.

---

### 🔹 Good Practice: Always Make Variables `private`
```java
public class Employee {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        } else {
            throw new IllegalArgumentException("Name cannot be empty");
        }
    }
}
```

✅ Protects data integrity, security, and flexibility.

