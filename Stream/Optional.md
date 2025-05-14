#java 

# ❓ Java `Optional` API — A Safer Way to Handle `null`

## 🧠 What is `Optional`?

> `Optional<T>` is a **container object** that may or may not contain a non-null value.

It helps you:

- Avoid `NullPointerException`
    
- Express **optional return values**
    
- Write cleaner, more expressive code

---

## 🧪 Why use `Optional`?

```java
// Traditional (Risky!)
String value = obj.getName(); // May be null -> NPE!

// Safer with Optional
Optional<String> maybeName = obj.getOptionalName();
maybeName.ifPresent(name -> System.out.println(name));
```
---

## 🧰 Creating Optionals

```java
Optional<String> name = Optional.of("Alice");         // Non-null only
Optional<String> maybeName = Optional.ofNullable(null); // Safe null wrapper
Optional<String> empty = Optional.empty();            // No value
```

---

## 🔍 Accessing the Value

```java
Optional<String> name = Optional.of("John");

// 1. ifPresent
name.ifPresent(n -> System.out.println(n));

// 2. orElse
String finalName = name.orElse("Default");

// 3. orElseGet (lazy)
String fromDB = name.orElseGet(() -> getFromDatabase());

// 4. orElseThrow
String result = name.orElseThrow(() -> new RuntimeException("No value!"));

// 5. get() (Not Recommended - throws if empty)
String bad = name.get(); // ⚠️ Use only when you're sure it's not empty
```

---

## 🔁 Transforming with `map()` and `flatMap()`

```java
Optional<String> name = Optional.of("  John  ");

String cleaned = name
    .map(String::trim)
    .map(String::toUpperCase)
    .orElse("DEFAULT"); // "JOHN"
```

📌 Use `flatMap()` if the function returns an `Optional`.

---

## 🔍 Filtering with `filter()`

```java
Optional<String> name = Optional.of("Alice");

name.filter(n -> n.startsWith("A"))
    .ifPresent(System.out::println); // Prints: Alice
```

---

## ✅ When to Use `Optional`

- ✔ Return value from a method **that may not return anything**
    
- ✔ Chain transformations safely
    
- ❌ Don’t use for fields/parameters in POJOs (causes more problems)

---

## 💡 Real Use Case

```java
public Optional<User> findUserById(int id) {
    return users.stream()
                .filter(u -> u.getId() == id)
                .findFirst(); // Returns Optional<User>
}
```

```java
findUserById(10)
    .map(User::getEmail)
    .ifPresent(email -> sendEmail(email));
```

---

## 🧠 Summary

|Operation|Purpose|
|---|---|
|`of()`|Wrap non-null value|
|`ofNullable()`|Wrap null or non-null|
|`get()`|Get value (avoid this unless sure)|
|`orElse()`|Default value if empty|
|`map()`|Transform inner value|
|`filter()`|Keep only if condition matches|
|`ifPresent()`|Run logic if value is present|
|`orElseThrow()`|Throw if empty|

