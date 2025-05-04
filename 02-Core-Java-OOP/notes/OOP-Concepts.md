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

🔹 Accessing Parent Members via super()
-	super() is used to call the constructor or methods of the parent class.
```java
class Animal {
    Animal() {
        System.out.println("Animal created");
    }
}

class Dog extends Animal {
    Dog() {
        super();  // Calls Animal constructor
        System.out.println("Dog created");
    }
}
```
🔹 Private Members: Use Getters/Setters
```java
class Animal {
    private String name = "Dog";

    public String getName() {
        return name;
    }
}

class Dog extends Animal {
    void printName() {
        System.out.println(getName()); // Use getter to access private field
    }
}
```

🔹 Protected Members: Accessible in Subclass
```java
class Animal {
    protected int age = 5;
}

class Dog extends Animal {
    void showAge() {
        System.out.println("Age is: " + age);  // Directly accessible
    }
}
```

🔹 💠 Diamond Problem in Java (with Interfaces)

Java doesn’t allow multiple class inheritance to avoid ambiguity (the Diamond Problem), but it can occur with interfaces if not handled properly.
```java
interface A {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    public void greet() {
        A.super.greet(); // Must specify which greet() to use
    }
}
```
- Java forces you to override and resolve ambiguity manually when implementing multiple interfaces with the same default method.

## 3. Polymorphism

Polymorphism means “many forms” — it allows one interface or method to behave differently based on the object that implements or invokes it.

In Java, polymorphism is of two main types:

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
What it is:

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

Abstraction is the concept of hiding implementation details and showing only the essential features to the user.

### Using Abstract Classes
-	Cannot be instantiated.
-	Can have constructors, fields, and both abstract and concrete methods.
-	Good when classes share common functionality but also need to define their own specific behavior.
  
```java
abstract class Shape {
    abstract void draw(); //abstract method
}

class Circle extends Shape {
    void draw() { System.out.println("Drawing Circle"); }
}
```
### Using Interfaces
-	Pure abstraction (until Java 8).
-	Cannot have constructors or instance fields.
-	All methods are abstract by default (until Java 8+ allowed default/static methods).
-	A class can implement multiple interfaces, unlike abstract classes.

```text
| Feature                       | Interface                         | Abstract Class                  |
|-------------------------------|-----------------------------------|---------------------------------|
| Can have constructors         | ❌ No                             | ✅ Yes                          |
| Supports multiple inheritance | ✅ Yes                            | ❌ No                           |
| Fields                        | `public static final` only        | Instance fields allowed         |
| Methods                       | Abstract, `default`, `static`     | Abstract and concrete methods   |
| Inheritance                   | `implements` (can be many)        | `extends` (only one)            |

```
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

💥  ***Real-world Edge Case: Method Added in Production***

Let’s say your interface is used in 20 different classes:
```java
interface Printer {
    void print();
}
```
✅ All working fine…

Then, you add a new method:
```java
interface Printer {
    void print();
    void scan(); // ⚠️ This breaks all implementing classes!
}
```
Now every implementing class must implement scan() or the code won’t compile — a breaking change in production.

Solution: Use default Methods (Java 8+)
```java
interface Printer {
    void print();

    default void scan() {
        System.out.println("Default scan implementation");
    }
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
