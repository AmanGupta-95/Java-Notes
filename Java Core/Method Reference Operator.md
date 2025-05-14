#java 

# 🔁 What does `::` mean?

That’s called the **method reference operator**.

Instead of writing:

```java
x -> System.out.println(x)
```

You can simply write:

```java
System.out::println
```

It's just **shorthand for lambda** when you're directly passing a method.

✅ Examples:

```java
list.forEach(System.out::println);         // prints each item
list.stream().map(String::toUpperCase);    // converts to uppercase
```

