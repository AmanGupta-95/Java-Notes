#java 

# 🕵️ What are Proxies in Spring?

---

## 🤔 Definition

> A **proxy** is a design pattern where one object acts as an **interface to another object**.

In Spring, **proxies wrap your beans** to add **extra behavior** (like logging, transactions, security, etc.) without modifying the original class.

---

## ⚙️ Why Does Spring Use Proxies?

✅ Common reasons:

- **AOP (Aspect-Oriented Programming)** — e.g., logging, auditing
    
- **Method-level security** — e.g., `@PreAuthorize`
    
- **Transactions** — e.g., `@Transactional`
    
- **Lazily loading beans**

---

## 🧰 Two Types of Proxies in Spring

|Type|Description|Used When|
|---|---|---|
|**JDK Dynamic Proxy**|Interface-based proxy|If your bean implements an interface|
|**CGLIB Proxy**|Class-based proxy using bytecode|If your bean does **not** implement any interface|

---

## 🧪 Example: AOP Logging Proxy

Let’s say you want to log before and after a method is called:

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore() {
        System.out.println("⏱ Method is about to be called");
    }

    @After("execution(* com.example.service.*.*(..))")
    public void logAfter() {
        System.out.println("✅ Method has been called");
    }
}
```

> This works because Spring **wraps your service with a proxy** that adds the log statements.

---

## 🧠 Key Concept: You Call the Proxy, Not the Actual Bean

```java
@Service
public class MyService {
    public void doSomething() {
        System.out.println("Doing something important");
    }
}
```

Spring creates a **proxy** like:

```
Proxy → MyService.doSomething()
```

The proxy decides:

- Should I add logging?
    
- Is this method transactional?
    
- Should I proceed to the actual object?

---

## 🧱 When Does It Break?

Spring proxies only work **if Spring controls the bean**. If you manually instantiate the class using `new`, **Spring cannot proxy it.**

```java
MyService s = new MyService(); // ❌ No proxy = no AOP, no transactions, etc.
```

---

## 🧩 Real Use Case – `@Transactional`

```java
@Service
public class BankService {

    @Transactional
    public void transfer() {
        // proxy starts transaction
        // method executes
        // proxy commits/rolls back transaction
    }
}
```

---

## ✅ Summary

|Term|Description|
|---|---|
|Proxy|Wrapper around a bean to add behavior|
|JDK Proxy|Used for interfaces|
|CGLIB Proxy|Used for concrete classes|
|Used In|AOP, Transactions, Security, Lazy beans|