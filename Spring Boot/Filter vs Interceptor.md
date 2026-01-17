#java 

# Filter vs Interceptor (Spring Boot)

## 📌 High-Level Idea

Both **Filter** and **Interceptor** are used to **intercept HTTP requests and responses**, but they operate at **different layers** of the request lifecycle.

---

## 🧩 Filter

### 🔹 What is a Filter

- A **Servlet-level** component
    
- Executes **before request reaches Spring**
    
- Part of **Java Servlet API**
    

---

### 🔹 Package
```java
javax.servlet.Filter
```

(or `jakarta.servlet.Filter` in newer versions)

---

### 🔹 Lifecycle

```java
Client
  ↓
Filter
  ↓
DispatcherServlet
  ↓
Controller
```

---

### 🔹 Methods

```java
void init()
void doFilter()
void destroy()
```

---

### 🔹 Example

```java
@Component
public class LoggingFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request,
                         ServletResponse response,
                         FilterChain chain)
            throws IOException, ServletException {

        System.out.println("Request received");
        chain.doFilter(request, response);
        System.out.println("Response sent");
    }
}
```

---

### 🔹 Typical Use Cases

- Authentication (JWT, API key)
    
- Request/Response logging
    
- CORS handling
    
- Input sanitization
    
- Compression
    

---

## 🧩 Interceptor

### 🔹 What is an Interceptor

- A **Spring MVC** component
    
- Works **after DispatcherServlet**
    
- Has access to **Handler (Controller + Method)**
    

---

### 🔹 Package

```java
org.springframework.web.servlet.HandlerInterceptor
```

---

### 🔹 Lifecycle

```java
Client
  ↓
Filter
  ↓
DispatcherServlet
  ↓
Interceptor
  ↓
Controller
```

---

### 🔹 Methods

```java
boolean preHandle()
void postHandle()
void afterCompletion()
```

---

### 🔹 Example

```java
@Component
public class AuthInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request,
                             HttpServletResponse response,
                             Object handler) {
        System.out.println("Before Controller");
        return true;
    }
}
```

---

### 🔹 Register Interceptor

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new AuthInterceptor());
    }
}
```

---

### 🔹 Typical Use Cases

- Authorization based on roles
    
- User context setup
    
- Audit logging
    
- Performance metrics
    
- Controller-level validation
    

---

## ⚔️ Filter vs Interceptor (Core Differences)

|Feature|Filter|Interceptor|
|---|---|---|
|Level|Servlet|Spring MVC|
|Runs before DispatcherServlet|✅|❌|
|Runs before Controller|✅|✅|
|Access to Controller|❌|✅|
|Access to Handler Method|❌|✅|
|Framework dependency|Servlet API|Spring|
|Typical usage|Security, logging|Business logic|

---

## 🧠 Execution Order (Very Important)

```scss
Filter (Request)
  → Interceptor.preHandle()
    → Controller
  → Interceptor.postHandle()
  → Interceptor.afterCompletion()
Filter (Response)
```

## 🧪 Interview Tricky Questions

### Q1: Can Interceptor replace Filter?

❌ No  
Interceptor cannot handle:

- CORS
    
- Low-level security
    
- Raw request manipulation
    

---

### Q2: Can Filter access Controller?

❌ No  
Filter has **no idea** which controller or method is invoked.

---

### Q3: Where should JWT validation go?

✅ **Filter**  
(Because authentication must happen before Spring processing)

---

### Q4: Where should role-based access go?

✅ **Interceptor**  
(Because it depends on controller/method metadata)

---

## 🎯 When to Use What

### ✅ Use Filter when:

- Working with **raw HTTP**
    
- Security, logging, CORS
    
- Need framework-agnostic logic
    

### ✅ Use Interceptor when:

- Need **controller awareness**
    
- Authorization
    
- Request-scoped business logic
    

---

## ⭐ One-line Interview Answer

> Filters work at the servlet level before Spring processes the request, while interceptors work inside Spring MVC and can access controllers and handler methods.