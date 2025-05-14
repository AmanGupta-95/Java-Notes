#java 

---

# 🌱 Spring Boot – Introduction

---

## 🚀 What is Spring Boot?

> **Spring Boot** is a Java framework that helps you **build stand-alone, production-ready** Spring applications with minimal setup.

✅ Makes it easier to:

- Run embedded servers (like Tomcat)
    
- Auto-configure components
    
- Focus on writing business logic, not boilerplate

---

## 🎯 Goals of Spring Boot

- Zero XML config
    
- Embedded servers (Tomcat, Jetty)
    
- Production-ready features (metrics, health checks)
    
- Auto-configuration
    
- Easy to test and deploy

---

## 📦 Spring Boot Project Structure

```bash
📁 src
 └─ 📁 main
     └─ 📁 java
         └─ 📦 com.example.demo
             ├── DemoApplication.java  # Main app
             ├── controller/
             ├── service/
             └── repository/
     └─ 📁 resources
         ├── application.properties    # Configuration
         └── static/ & templates/      # (for web apps)
```

---

## 🧱 Create a Simple Spring Boot App

```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

✅ `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`

---

## 🎤 Create a REST Controller

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }
}
```

Output:

```bash
GET http://localhost:8080/hello
→ "Hello, Spring Boot!"
```

---

## ⚙️ application.properties

Configure your app here:

```properties
server.port=8081
spring.application.name=my-app
```

---
## 🛠 Tools You’ll Commonly Use

|Tool|Use case|
|---|---|
|`@RestController`|Create REST APIs|
|`@Service`|Business logic|
|`@Repository`|Data access (e.g. DB)|
|`@Autowired`|Inject dependencies|
|`application.properties`|Configuration file|

---

## 🧪 Dependencies You Often Add

In your `pom.xml` or via Spring Initializr:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## ✅ Summary

- Spring Boot = Spring + auto-magic setup
    
- No need for XML or external server
    
- Start with `@SpringBootApplication` and build from there
    
- Create REST APIs easily using `@RestController`
