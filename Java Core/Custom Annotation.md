#java #annotation 

## 🧠 How to Create Custom Annotations in Java?

---
# 📌 TL;DR:

|Aspect|Summary|
|---|---|
|Create Annotation|`@interface` keyword|
|Define Target|`@Target(ElementType.TYPE/FIELD/METHOD)`|
|Define Retention|`@Retention(RetentionPolicy.RUNTIME)`|
|Read at Runtime|Using Java Reflection|

---
# 1. Basics of Custom Annotations

✅ You can create your own annotations using `@interface` keyword.

✅ You can control **where** the annotation can be used with **meta-annotations** like:

|Meta-Annotation|Purpose|
|---|---|
|`@Target`|Where the annotation can be applied (class, method, field, etc.)|
|`@Retention`|When the annotation is available (Compile-time or Runtime)|
|`@Documented`|Whether it appears in Javadocs|
|`@Inherited`|Whether it can be inherited by child classes|

---

# 2. Step-by-Step Examples

---

## 🏷️ A. Custom Annotation for Classes

---

### Define the Annotation:

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.annotation.ElementType;

@Retention(RetentionPolicy.RUNTIME) // Available at Runtime
@Target(ElementType.TYPE)            // Only for Classes or Interfaces
public @interface Info {
    String author();
    String version();
}
```

---

### Use the Annotation:

```java
@Info(author = "John Doe", version = "1.0")
public class MyService {
    // Some service code
}
```

---

## 🏷️ B. Custom Annotation for Variables (Fields)

---

### Define the Annotation:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD) // Only for variables
public @interface Important {
    String value() default "High";
}
```

---

### Use the Annotation:

```java
public class User {
    @Important("Very High")
    private String password;

    private String username;
}
```

---
## 🏷️ C. Custom Annotation for Methods

---

### Define the Annotation:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD) // Only for methods
public @interface Execute {
    int times() default 1; // How many times to execute
}
```

---

### Use the Annotation:

```java
public class TaskRunner {
    
    @Execute(times = 3)
    public void runTask() {
        System.out.println("Running task...");
    }
}
```

# 🛠️ Bonus: Processing Annotations Using Reflection

---

Java’s **[[Reflection]] API** can **read and react** to these annotations at runtime!

Example:

```java
import java.lang.reflect.Method;

public class AnnotationProcessor {
    public static void main(String[] args) throws Exception {
        Class<TaskRunner> obj = TaskRunner.class;

        for (Method method : obj.getDeclaredMethods()) {
            if (method.isAnnotationPresent(Execute.class)) {
                Execute execute = method.getAnnotation(Execute.class);
                for (int i = 0; i < execute.times(); i++) {
                    method.invoke(obj.getDeclaredConstructor().newInstance());
                }
            }
        }
    }
}
```

Output:

```java
Running task...
Running task...
Running task...
```

✅ Here, based on `@Execute(times=3)`, the method is called **3 times**!