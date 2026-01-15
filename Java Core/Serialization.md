#java 

## 📌 What is Serialization

**Serialization** is the process of converting a **Java object into a byte stream** so that it can be:

- Saved to a file
    
- Sent over a network
    
- Stored in memory or cache
    

The reverse process is called **Deserialization**.

---

## 🔁 Serialization Flow

```vb
Object  →  Byte Stream  →  File / Network / DB
Byte Stream → Object   →  Deserialization
```

---

## 📦 Key Interface

`java.io.Serializable`

- Marker interface (no methods)
    
- JVM uses it to allow object serialization
    

---

## 🔹 Example

### Serializable Class

```java
import java.io.Serializable;

class Employee implements Serializable {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

---

### Serialization

```java
ObjectOutputStream oos =
    new ObjectOutputStream(new FileOutputStream("emp.ser"));

oos.writeObject(emp);
oos.close();
```

---

### Deserialization

```java
ObjectInputStream ois =
    new ObjectInputStream(new FileInputStream("emp.ser"));

Employee emp = (Employee) ois.readObject();
ois.close();
```

---

## 🧠 What Happens Internally

- JVM converts object state into **binary format**
    
- Class metadata is also stored
    
- On deserialization, JVM recreates object **without calling constructor**
    

---

## ⚠️ Important Rules

### 🔸 Serializable Required

```java
class A { }              // ❌ Not serializable
class B implements Serializable { }  // ✅
```

---

### 🔸 `transient` Keyword

- Prevents a field from being serialized

```java
transient String password;
```

### 🔸 Static Fields

- **Not serialized** (belong to class, not object)
    

---

## 🔑 `serialVersionUID`

### Why it exists

Ensures compatibility between serialized object and class version.

```java
private static final long serialVersionUID = 1L;
```

### If not defined

- JVM auto-generates one
    
- Class change → `InvalidClassException`
    

---

## 🧪 Example Problem

```java
class User implements Serializable {
    int id;
    transient String password;
}
```

Result:

- `id` → saved
    
- `password` → ignored
    

---

## 🚫 What is NOT Serialized

- Static variables
    
- Transient variables
    
- Constructors
    
- Methods
    

---

## 🔐 Security Concerns

- Deserialization can execute malicious code
    
- Never deserialize **untrusted data**
    
- Use validation / filters in production
    

---

## ⚔️ Serialization vs Deserialization

|Serialization|Deserialization|
|---|---|
|Object → bytes|Bytes → object|
|`writeObject()`|`readObject()`|
|Stores state|Restores state|

---

## 📌 When to Use Serialization

✅ Use cases:

- Distributed systems
    
- Caching (Redis, Hazelcast)
    
- Session replication
    
- Messaging (legacy systems)
    

❌ Avoid when:

- Performance critical paths
    
- Microservices (prefer JSON/Protobuf)
    

---

## ⭐ One-line Interview Answer

> Serialization converts an object into a byte stream for storage or transmission, and deserialization recreates the object from that stream.