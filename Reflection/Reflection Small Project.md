#java 

---

# 🛠️ Mini Project Upgrade: Warn if Important Fields are Empty (Null)

---

## 📂 Step 1: Custom Annotation (same as before)

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.annotation.ElementType;

// Define custom annotation
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.FIELD)
public @interface Important {
}
```

---

## 📂 Step 2: Java Class with Fields

```java
public class Product {
    @Important
    private String name;

    private double price;

    @Important
    private String category;

    public Product(String name, double price, String category) {
        this.name = name;
        this.price = price;
        this.category = category;
    }
}
```

---

## 📂 Step 3: Updated Reflection Processor

```java
import java.lang.reflect.Field;

public class ImportantFieldProcessor {

    public static void process(Object obj) throws Exception {
        Class<?> clazz = obj.getClass();

        for (Field field : clazz.getDeclaredFields()) {
            if (field.isAnnotationPresent(Important.class)) {
                field.setAccessible(true); // Access private fields
                Object value = field.get(obj);

                if (value == null) {
                    System.out.println("⚠️ Warning: Important field '" + field.getName() + "' is empty (null)!");
                } else {
                    System.out.println("✅ Important field: " + field.getName() + " = " + value);
                }
            }
        }
    }
}
```

✅ **If value is `null`**, it prints a ⚠️ **warning**.  
✅ **If value is present**, it prints ✅ normally.

---

## 📂 Step 4: Run the Application

```java
public class Main {
    public static void main(String[] args) throws Exception {
        Product product = new Product(null, 1500.00, "Electronics");
        ImportantFieldProcessor.process(product);
    }
}
```

---

### 🖥️ Output:

```
⚠️ Warning: Important field 'name' is empty (null)!
✅ Important field: category = Electronics
```

---
# 📚 What We Achieved?

|Feature|Benefit|
|---|---|
|Auto-scan @Important Fields|No need to hardcode validation manually|
|Dynamic Warning System|Automatically detects missing important data|
|Framework-like behavior|Just like Bean Validation in Spring/Hibernate|

---

# 📦 Full Project Structure (Final)

```
/Project
  |-- Important.java                (Annotation)
  |-- Product.java                   (Data class)
  |-- ImportantFieldProcessor.java   (Reflection Processor)
  |-- Main.java                      (Runner)

```

---

# 🧠 Extra Notes (Good for Interview)

> **Reflection + Custom Annotations** together allow Java frameworks to build:
> 
> - **Auto Validation**
>     
> - **Auto Mapping (Entity to DB)**
>     
> - **Auto Dependency Injection**


(For example: `@NotNull`, `@Autowired`, `@RequestMapping`)

---