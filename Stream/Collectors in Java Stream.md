#java 

# 🧰 Commonly Used `Collectors` in Java Stream API

---

## 🔁 1. `Collectors.toList()`

> Collects the stream elements into a `List`.

```java
List<String> names = Stream.of("Ram", "Shyam", "Radha")
                           .collect(Collectors.toList());
```

## 🔁 2. `Collectors.toSet()`

> Collects the elements into a `Set` (removes duplicates).

```java
Set<String> names = Stream.of("A", "B", "A", "C")
                          .collect(Collectors.toSet()); // ["A", "B", "C"]
```

## 📚 3. `Collectors.joining()`

> Joins stream elements into a single `String`.

```java
String result = Stream.of("Apple", "Banana", "Cherry")
                      .collect(Collectors.joining(", "));
// Output: Apple, Banana, Cherry
```

## 📊 4. `Collectors.counting()`

> Counts the number of elements in the stream.

```java
long count = Stream.of("A", "B", "C").collect(Collectors.counting());
// Output: 3
```

## 🧮 5. `Collectors.summingInt()`

> Calculates the sum of an `int` property.

```java
int totalPrice = products.stream()
                         .collect(Collectors.summingInt(p -> p.getPrice()));
```

📌 You can also use:

- `summingDouble()`
- `summingLong()`

## 📈 6. `Collectors.averagingInt()`

> Calculates the average of an `int` property.

```java
double avgPrice = products.stream()
                          .collect(Collectors.averagingInt(Product::getPrice));
```

## 🧵 7. `Collectors.groupingBy()`

> Groups data based on a key function (like SQL `GROUP BY`)

```java
Map<String, List<Product>> grouped = products.stream()
    .collect(Collectors.groupingBy(Product::getCategory));
```

## ✂️ 8. `Collectors.partitioningBy()`

> Splits stream into **two groups** based on a boolean condition (true/false)

```java
Map<Boolean, List<Product>> partitioned = products.stream()
    .collect(Collectors.partitioningBy(p -> p.getPrice() > 1000));
```

## 🎯 9. `Collectors.mapping()`

> Allows you to **transform values during grouping**

```java
Map<String, List<String>> nameByCategory = products.stream()
    .collect(Collectors.groupingBy(
        Product::getCategory,
        Collectors.mapping(Product::getName, Collectors.toList())
    ));
```

## 🎯 10. `Collectors.maxBy()` and `minBy()`

> Finds the max or min element based on a comparator.

```java
Optional<Product> max = products.stream()
    .collect(Collectors.maxBy(Comparator.comparing(Product::getPrice)));

Optional<Product> min = products.stream()
    .collect(Collectors.minBy(Comparator.comparing(Product::getPrice)));
```

## 🧠 Summary Table

|Function|Purpose|
|---|---|
|`toList()` / `toSet()`|Collect into collections|
|`joining()`|Combine strings|
|`counting()`|Count elements|
|`summingInt()`|Sum numeric field|
|`averagingInt()`|Average value|
|`groupingBy()`|Group by field|
|`partitioningBy()`|True/false split|
|`mapping()`|Transform values while collecting|
|`maxBy()` / `minBy()`|Get max or min element|
