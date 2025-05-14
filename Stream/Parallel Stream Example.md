#java 

# 🧠 Real-World Example: Filter and Group Products Using `parallelStream()`

---

## 📦 `Product.java`

```java
public class Product {
    private String name;
    private String category;
    private double price;

    // Constructor
    public Product(String name, String category, double price) {
        this.name = name;
        this.category = category;
        this.price = price;
    }

    // Getters
    public String getName() { return name; }
    public String getCategory() { return category; }
    public double getPrice() { return price; }

    @Override
    public String toString() {
        return name + " - ₹" + price;
    }
}
```

---

## 🧪 `ProductAnalysis.java`

```java
import java.util.*;
import java.util.stream.Collectors;

public class ProductAnalysis {
    public static void main(String[] args) {
        List<Product> products = Arrays.asList(
            new Product("iPhone", "Electronics", 80000),
            new Product("Samsung TV", "Electronics", 45000),
            new Product("Banana", "Grocery", 40),
            new Product("Milk", "Grocery", 60),
            new Product("T-shirt", "Clothing", 1200),
            new Product("Jeans", "Clothing", 2500)
        );

        // 🔍 Filter expensive products and group by category
        Map<String, List<Product>> expensiveProductsByCategory =
            products.parallelStream()
                    .filter(p -> p.getPrice() > 1000) // Expensive
                    .collect(Collectors.groupingBy(Product::getCategory));

        // 🖨️ Display result
        expensiveProductsByCategory.forEach((category, items) -> {
            System.out.println("\n📂 " + category);
            items.forEach(System.out::println);
        });
    }
}
```

🖥️ Sample Output:
```
📂 Electronics
iPhone - ₹80000
Samsung TV - ₹45000

📂 Clothing
T-shirt - ₹1200
Jeans - ₹2500
```

## 🔍 What Happened?

- Used `parallelStream()` on a list of `Product` objects
    
- Filtered products where `price > 1000`
    
- Grouped results by `category` using `Collectors.groupingBy()`
    
- Printed results by category

## 🧠 Use Cases in Real Apps

|Use Case|How Stream Helps|
|---|---|
|Filter expensive/discounted products|`filter()`|
|Group products by category, brand, etc.|`groupingBy()`|
|Sort by price|`sorted(Comparator.comparing())`|
|Search specific items|`filter()` + `findAny()` / `findFirst()`|
|Count items by type|
