#java 
# 🌿 Spring Core – Basics

---

## 🌟 What is Spring Core?

> Spring Core provides the **Inversion of Control (IoC)** and **Dependency Injection (DI)** features that manage your app's components (called _beans_) automatically.

✅ You don’t create and wire dependencies manually — Spring does it for you!

---

## 🔁 Inversion of Control (IoC)

**Normal approach (tight coupling):**

```java
Car car = new Car(new Engine()); // Manual creation
```

Spring approach (loose coupling):

```java
@Component
public class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

➡️ Spring creates the `Engine` object and injects it into `Car`.

---

## 🧩 Key Annotations in Spring Core

|Annotation|Description|
|---|---|
|`@Component`|Marks a class as a Spring-managed bean|
|`@Service`|Specialized `@Component` for service layer|
|`@Repository`|Specialized `@Component` for DB/repo layer|
|`@Controller`|Specialized `@Component` for MVC (used with UI)|
|`@RestController`|Shortcut for `@Controller + @ResponseBody`|
|`@Autowired`|Automatically injects the required dependency|

---

## 🛠 Example: DI with @Component and @Autowired

```java
@Component
public class Engine {
    public String start() {
        return "Engine started!";
    }
}

@Component
public class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        System.out.println(engine.start());
    }
}
```

---

## ✅ Auto-Wiring a Component in Main App

```java
@SpringBootApplication
public class MyApp implements CommandLineRunner {

    @Autowired
    private Car car;

    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }

    @Override
    public void run(String... args) {
        car.drive();
    }
}
```

## ⚙️ How It Works Behind the Scenes

1. Spring scans the package using `@ComponentScan`.
    
2. It finds `@Component`, `@Service`, etc., and creates **Beans**.
    
3. It wires them using `@Autowired`.

---

## ☑️ Tip

You can only `@Autowired` a bean that Spring knows (i.e., has `@Component`, `@Service`, etc., or is registered manually).

---