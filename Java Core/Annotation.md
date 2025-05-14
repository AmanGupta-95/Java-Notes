#java  #annotation

## 🧠 What are Annotations in Java?

---
# 📌 TL;DR:

|Aspect|Summary|
|---|---|
|What?|Labels/instructions for Java/frameworks|
|Why?|Reduces boilerplate, improves readability|
|Where used?|Everywhere! (Spring Boot, Lombok, Hibernate)|
|How works?|Reflection, compile-time processing

---
### 🔹 Simple Definition

> 🏷️ **Annotations are special labels or tags** you attach to classes, methods, variables, etc., to **give instructions** to the Java compiler or a framework (like Spring Boot).

✅ They **add extra behavior** **without changing** the actual business logic.

---

### 🔸 Example:

```java
class Car {
    @Override
    public String toString() {
        return "This is a car";
    }
}
```
- `@Override` tells Java:  
    "**Hey! This method should override a method from the parent class.**"
- If you make a mistake, the compiler will show an error.

---

## 🎯 Why Annotations are Important?

- They **reduce boilerplate code** (especially with Lombok).
- They **tell frameworks** like Spring Boot how to wire things automatically (Dependency Injection, REST APIs, etc.).
- They make code more **declarative** and **readable**.

---

# 🛠️ Basic Categories of Annotations

---

|Category|Examples|Purpose|
|---|---|---|
|Built-in Java|`@Override`, `@Deprecated`|Compiler instructions|
|User-defined|(Custom annotations)|Create your own|
|Framework-specific|`@SpringBootApplication`, `@Autowired`, `@Entity`, `@Service`|Used by frameworks like Spring|
|Lombok Annotations|`@Getter`, `@Setter`, `@AllArgsConstructor`|Auto-generate code like getters, constructors|

---

# 🔥 Popular Annotations Examples (Spring Boot + Lombok)

---

### 📌 Spring Boot Annotations

|Annotation|Purpose|
|---|---|
|`@SpringBootApplication`|Marks main class for Spring Boot app|
|`@RestController`|Makes a class a REST API controller|
|`@RequestMapping`|Maps HTTP requests to methods|
|`@Autowired`|Injects dependency automatically|
|`@Service`|Marks a class as a service layer component|
|`@Entity`|Marks a class as a database table model|

---

### 📌 Lombok Annotations

|Annotation|Purpose|
|---|---|
|`@Getter`|Auto-generates getter methods|
|`@Setter`|Auto-generates setter methods|
|`@NoArgsConstructor`|Auto-generates no-argument constructor|
|`@AllArgsConstructor`|Auto-generates all-arguments constructor|
|`@Builder`|Auto-generates builder pattern methods|

---

# 🧩 How Annotations Actually Work?

✅ Annotations are processed at **compile time** or **runtime** using:

- **Reflection** (Java can look at classes, methods, fields during runtime).
- **Frameworks** like Spring Boot scan your code for annotations and create objects/configurations automatically.

---

# 🛠️ Small Practical Example (Spring Boot Controller)

```java
@RestController
@RequestMapping("/api")
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```
- `@RestController`: Marks the class as REST API.
- `@RequestMapping("/api")`: All APIs under `/api`.
- `@GetMapping("/hello")`: `/api/hello` will return "Hello, World!".