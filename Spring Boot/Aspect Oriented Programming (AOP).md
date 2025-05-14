#java

# 🧩 Spring AOP – Aspect-Oriented Programming

---

## 🤔 What is AOP?

> AOP is a programming paradigm that helps you modularize **cross-cutting concerns** — logic that spans multiple parts of your application.

🧱 Examples of cross-cutting concerns:

- Logging
    
- Security checks
    
- Caching
    
- Transaction management
    
- Performance monitoring

---

## 🧠 Core Concepts in AOP

|Term|Meaning|
|---|---|
|**Aspect**|A class that contains cross-cutting logic|
|**Join Point**|A specific point in execution (e.g. method call) where advice can run|
|**Advice**|The actual action taken at a join point (e.g. logging, auth check)|
|**Pointcut**|Expression to match join points (like method patterns)|
|**Weaving**|The process of applying aspects to the target objects (via proxies)|

---

## 🧪 Basic Example of Logging Aspect

```java
@Aspect
@Component
public class LoggingAspect {

    // Pointcut: all methods in service package
    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("➡️ Calling: " + joinPoint.getSignature());
    }

    @After("execution(* com.example.service.*.*(..))")
    public void logAfter(JoinPoint joinPoint) {
        System.out.println("✅ Finished: " + joinPoint.getSignature());
    }
}
```

> `@Aspect` marks the class as an **aspect**  
> `@Before` and `@After` are **advices**  
> The `execution(...)` is the **pointcut**

---

## 🧩 Types of Advice

|Advice Type|Description|
|---|---|
|`@Before`|Runs **before** the target method|
|`@After`|Runs **after** the target method (regardless of outcome)|
|`@AfterReturning`|Runs **after successful** method execution|
|`@AfterThrowing`|Runs **after method throws** an exception|
|`@Around`|Runs **before and after**; full control over the method|

---

## 💡 Example: `@Around` Advice

```java
@Aspect
@Component
public class TimingAspect {

    @Around("execution(* com.example.service.*.*(..))")
    public Object measureExecutionTime(ProceedingJoinPoint pjp) throws Throwable {
        long start = System.currentTimeMillis();
        Object result = pjp.proceed(); // call the actual method
        long end = System.currentTimeMillis();

        System.out.println("⏱ " + pjp.getSignature() + " took " + (end - start) + "ms");
        return result;
    }
}
```

---

## 🔧 Enabling AOP in Spring Boot

No extra config needed if you're using `spring-boot-starter`.  
Just make sure:

```java
@SpringBootApplication
@EnableAspectJAutoProxy
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

---

## 🚫 AOP Limitation: Self-Invocation

Spring AOP only works if the **call passes through the proxy**.

```java
@Service
public class MyService {
    
    @Transactional // ✅ works when called externally
    public void methodA() {}

    public void methodB() {
        methodA(); // ❌ no proxy here; transactional won't apply
    }
}
```

## ✅ Summary

- AOP helps **separate cross-cutting concerns**
    
- Spring uses **proxies** to apply AOP
    
- Advices are methods that run **before/after/around** target methods
    
- Pointcuts define **where** to apply the advice