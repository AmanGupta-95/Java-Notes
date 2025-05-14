#java  #static 
### 🔹 What does `static` mean in Java?

In Java, `static` means **"belonging to the class, not to any specific object."**

Normally, when you create an object using `new`, you access its **instance methods** or **variables**. But if something is marked as `static`, you **don't need to create an object** — you can access it directly using the class name.

---

### 🔸 1. Static Variable (Class Variable)

A static variable is **shared** among all objects of the class.

```java
public class Car { 

	static int wheels = 4; // Shared by all cars     
	String color;      
	
	public Car(String color) {         
		this.color = color;     
	} 
}
```

✅ Usage:

```java
System.out.println(Car.wheels); // Output: 4
```



---

### 🔸 2. Static Method

A static method can be called **without creating an object** of the class.


```java
public class MathUtils {     // A static method     
	public static int square(int x) {         
		return x * x;     
	} 
}
```

✅ Usage:


```java
int result = MathUtils.square(5); // Output: 25
```

🔹 Note: Static methods **can't use non-static variables** directly, because they don't belong to any object.

---

### 🔸 3. Static Block

A static block runs **once** when the class is loaded. Used for initializing static data.

```java
public class AppConfig {     
	static String appName;      
	static {         
		appName = "My Cool App";         
		System.out.println("Static block called!");     
	} 
}
```

✅ Usage:

```java
System.out.println(AppConfig.appName);
```

---

### 🔸 4. Static Class (Nested)

In Java, you can make a **nested class** static.

```java
public class Outer {     
	static class Inner {         
		void sayHi() {             
			System.out.println("Hello from static nested class!");         
		}     
	} 
}
```

✅ Usage:

```java
Outer.Inner inner = new Outer.Inner(); inner.sayHi(); // Output: Hello from static nested class!
```

---

### 🧠 Summary

|Keyword|Belongs To|Accessed With|Memory Shared?|
|---|---|---|---|
|static variable|Class|ClassName.varName|✅ Yes|
|static method|Class|ClassName.method()|✅ Yes|
|static block|Class|Auto runs on load|✅ Yes|
|static class|Class|OuterClass.InnerClass|✅ Yes|