# 🧱 Object-Oriented Programming (OOP) Concepts in Java

OOP is a programming paradigm based on the concept of "objects", which can contain data and code.

---

##  1. Classes and Objects

###  Class
A blueprint or template for creating objects.

A `class` defines a blueprint, and an `object` is an instance of that class.

```java
class User {
    String name;
    int age;
}
User u = new User();
```
##  Edge Cases & Gotchas:
-	Accessing fields without initialization can lead to default values (e.g., 0, null, false).
-	Objects must be created using new. Forgetting new leads to NullPointerException when accessing fields or methods.


```java
User u = null;
System.out.println(u.name); // NullPointerException
```
## 2. Inheritance

 What it is:

Allows one class (child) to inherit the behavior and attributes of another (parent).
```java
class Animal {
    void makeSound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Woof!"); }
}
```
### Edge Cases & Gotchas:
-	Constructors are not inherited, only accessible via super().
-	Private members are not inherited—you need to use protected or getters/setters.
-	Diamond problem is not applicable in Java (due to no multiple inheritance with classes), but can occur with interfaces.

## 3. Polymorphism

### Overloading (compile-time polymorphism)
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```
### Overriding (runtime polymorphism)
```java
class Animal {
    void sound() { System.out.println("Animal"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Dog"); }
}
```
### Edge Cases & Gotchas:
-	Overriding static methods doesn’t work — it’s called method hiding.
-	You cannot override final or private methods.
-	Always use @Override annotation to catch overriding errors at compile time.
```java
class A {
    static void greet() { System.out.println("Hi"); }
}
class B extends A {
    static void greet() { System.out.println("Hello"); } // Method hiding
}
```
## 4. Encapsulation
 ###hat it is:

Encapsulation hides internal data using private access and exposes it using public methods.
```java
class Account {
    private int balance = 1000;

    public int getBalance() { return balance; }
    public void setBalance(int amount) {
        if (amount >= 0) this.balance = amount;
    }
}
```
### Edge Cases & Gotchas:
-	Avoid exposing internal fields with public access (public int balance) — it breaks encapsulation.
-	Setters should include validation logic to protect object state.
-	Beware of mutable fields like lists—always return copies when exposing them.
```java
private List<String> items = new ArrayList<>();

public List<String> getItems() {
    return new ArrayList<>(items); // Prevent direct modification
}
```
## 5. Abstraction

### Using Abstract Classes
```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() { System.out.println("Drawing Circle"); }
}
```
### Using Interfaces
```java
interface Drawable {
    void draw();
}

class Square implements Drawable {
    public void draw() { System.out.println("Drawing Square"); }
}
```
### Edge Cases & Gotchas:
-	Abstract classes can have constructors, interfaces cannot.
-	A class can implement multiple interfaces but can extend only one class.
-	If you add a new method to an interface in production, all implementing classes will break unless you use default methods (Java 8+).
```java
interface Printer {
    default void printInfo() { System.out.println("Default print"); }
}
```
### Summary Table (with Gotchas)
```text
| Concept          | Description                           | Edge Case / Warning                              |
|------------------|---------------------------------------|--------------------------------------------------|
| Class & Object   | Blueprint and instances               | Don’t use uninitialized objects                  |
| Inheritance      | Reuse parent properties               | Private members aren’t inherited                 |
| Polymorphism     | Multiple forms of a method            | Static methods can’t be overridden               |
| Encapsulation    | Data hiding via private + accessors   | Validate setters, protect internal state         |
| Abstraction      | Focus on what, not how                | Interface updates can break many classes         |
```
✅ Next: [Java Collections Framework](Java-Collections.md)