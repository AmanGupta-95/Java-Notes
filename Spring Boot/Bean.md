#java 

# 🌱 Spring Bean Lifecycle

---

## 🤖 What is a Spring Bean?

> A **Bean** is simply an object that is managed by the **Spring container**.

✅ Created from a class annotated with `@Component`, `@Service`, `@Repository`, etc.

---

## 🔄 Lifecycle of a Spring Bean

Spring manages a bean through the following steps:

```mahthematica
1️⃣ Instantiation
2️⃣ Populate properties (Dependency Injection)
3️⃣ Set Bean Name
4️⃣ Set Bean Factory
5️⃣ Set Application Context
6️⃣ PostConstruct methods
7️⃣ Initialization logic
8️⃣ Ready to use
9️⃣ PreDestroy method
🔟 Destruction
```

---

## 📜 Ways to Hook into the Lifecycle

### 1. **Using `@PostConstruct` and `@PreDestroy`**

```java
@Component
public class ExampleBean {

    @PostConstruct
    public void init() {
        System.out.println("Bean is initialized ✅");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Bean is being destroyed 🗑️");
    }
}
```

> 🔧 `@PostConstruct` and `@PreDestroy` are from `jakarta.annotation` or `javax.annotation`.

---

### 2. **Implementing `InitializingBean` and `DisposableBean`**

```java
@Component
public class ExampleBean implements InitializingBean, DisposableBean {

    @Override
    public void afterPropertiesSet() {
        System.out.println("Bean initialization logic here");
    }

    @Override
    public void destroy() {
        System.out.println("Cleanup before bean is destroyed");
    }
}
```

### 3. **Using `@Bean(initMethod, destroyMethod)` in Configuration**

```java
@Configuration
public class AppConfig {

    @Bean(initMethod = "start", destroyMethod = "stop")
    public Engine engine() {
        return new Engine();
    }
}
```

```java
public class Engine {
    public void start() {
        System.out.println("Engine started");
    }

    public void stop() {
        System.out.println("Engine stopped");
    }
}
```

## 🚫 Important

To trigger `@PreDestroy`, your application must shut down _gracefully_. If you force stop the app (e.g. Ctrl+C quickly), the destroy hooks may not execute.

---

## 🧠 Summary

|Hook Method|When it's Called|
|---|---|
|`@PostConstruct`|After DI, before use|
|`afterPropertiesSet()`|Same as `@PostConstruct`|
|`@PreDestroy`|Before the bean is removed|
|`destroy()`|Same as `@PreDestroy`|
|`@Bean(initMethod)`|Custom init method|
|`@Bean(destroyMethod)`|Custom destroy method|

