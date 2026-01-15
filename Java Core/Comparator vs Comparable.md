#java 

## 📌 Overview

Both **Comparable** and **Comparator** are used to **define sorting logic** in Java.  
The key difference is **where and how** the sorting logic is written.

---

## 🧩 Comparable

### 🔹 What it is

- An **interface** used to define **natural ordering** of objects
    
- Sorting logic is written **inside the class itself**

### 🔹 Package

`java.lang`

### 🔹 Method

`int compareTo(T o)`

### 🔹 When to use

- When there is **only one logical way** to sort an object
    
- Example: sort `Employee` by `id` or `Student` by `rollNo`
    

---

### 🔹 Example


``` java
class Employee implements Comparable<Employee> {
    int id;
    String name;

    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public int compareTo(Employee other) {
        return this.id - other.id; // sort by id
    }
}

```

`Collections.sort(employeeList);

---

### ✅ Pros

- Simple
    
- No extra class needed
    

### ❌ Cons

- Only **one sorting logic**
    
- Modifies the original class (not always allowed)
    

---

## 🧩 Comparator

### 🔹 What it is

- An **interface** used to define **custom or multiple sorting strategies**
    
- Sorting logic is written **outside the class**
    

### 🔹 Package

`java.util`

### 🔹 Method

`int compare(T o1, T o2)`

### 🔹 When to use

- When you need **multiple sorting criteria**
    
- When you **cannot modify** the source class
    

---

### 🔹 Example

```java
class Employee {
    int id;
    String name;

    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

```java
class NameComparator implements Comparator<Employee> {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.name.compareTo(e2.name);
    }
}
```

`Collections.sort(employeeList, new NameComparator());`

---

### 🔹 Lambda Example (Modern Java)

`employeeList.sort((e1, e2) -> e1.name.compareTo(e2.name));`

---

### ✅ Pros

- Multiple sorting logics
    
- No change to original class
    
- Cleaner with lambdas
    

### ❌ Cons

- Slightly more code (without lambdas)
    

---

## ⚔️ Comparable vs Comparator (Quick Comparison)

|Feature|Comparable|Comparator|
|---|---|---|
|Package|`java.lang`|`java.util`|
|Method|`compareTo()`|`compare()`|
|Sorting logic|Inside class|Outside class|
|Number of strategies|One|Multiple|
|Modifies class|Yes|No|
|Used by|`Collections.sort(list)`|`Collections.sort(list, comparator)`|