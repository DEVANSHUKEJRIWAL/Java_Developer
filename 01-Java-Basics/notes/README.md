# 📝 Java Basics Notes

##  Syntax & Structure
- Every Java program starts with a `class`.
- The entry point is the `main()` method.
- The class encapsulates the behavior and properties of an object.

```java

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### What does public static void main(String[] args) mean?
	1.	public: This is an access modifier that makes the main() method accessible from anywhere, allowing the Java runtime environment to call it. If public is omitted, it would be package-private by default, meaning it wouldn’t be accessible outside the package.
	2.	static: This means the main() method belongs to the class itself and not to an instance of the class. The Java runtime doesn’t create an instance of the class before calling main(), so it must be static.
	3.	void: The main() method doesn’t return anything, which is why it’s declared as void. The program doesn’t need to send a return value back to the operating system when it finishes executing.
	4.	main: This is the name of the method. The Java runtime looks specifically for a method named main to start program execution.
	5.	String[] args: This parameter represents an array of String objects. When you run a Java program from the command line, any command-line arguments passed to the program are captured as strings in this array. For example, if you run java HelloWorld arg1 arg2, args will contain ["arg1", "arg2"].

### What happens if public static void main(String[] args) is not there?

If there is no main() method, Java won’t know where to start the program, and the program cannot be run directly. However, there are scenarios where the main() method is not required:
1.	**In GUI applications**: Some applications (like Swing or JavaFX) may use a different entry point, like a constructor or a separate thread, to start the application. But even in these cases, a main() method is often still included as a starting point.
2.	**In applets (deprecated)**: Old applets used init() or start() methods to initiate execution. However, Java applets are largely deprecated in modern Java versions.
3.	**For unit testing**: If you’re writing test cases using frameworks like JUnit, a main() method is not necessary because the testing framework takes care of running the tests.

### How can we start a program if there is no main() method?

Without the main() method, you can’t run a standard Java program. However, in some cases, the program can start in different ways:
1.	**Web applications**: Frameworks like Spring Boot provide their own entry points (e.g., @SpringBootApplication) to run the application, often via a command-line tool like mvn spring-boot:run.
2.	**Servlets**: In a web server context, a servlet (which is a class that extends HttpServlet) doesn’t require a main() method. The web server runs it by mapping HTTP requests to the servlet class’s doGet() or doPost() methods.
3.	**JavaFX and Swing**: In desktop GUI applications, you often use a launch() method (in JavaFX) or a custom entry point for GUI initialization, although you can still have a main() method to start the application.

### What happens if we omit parts of public static void main(String[] args)?

1. **If public is omitted**:
   1. The main() method becomes package-private (default access level).
   2. 	This means it can only be accessed by other classes within the same package. The Java runtime cannot access it if it is not public, and your program will not run.
   3.	Example:
   ```java
   class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
   }
In this case, the program will fail to run because the main() method isn’t marked as public.

2. **If static is omitted**:
   1.	The main() method becomes non-static.
   2.	You cannot call a non-static method from the class without creating an instance of the class first. Since the Java runtime doesn’t create an instance of the class before calling the main() method, it will result in a compilation error.
   3.	Example:
   ```java
   public class HelloWorld {
    public void main(String[] args) {  // Without static
        System.out.println("Hello, World!");
    }
   }
   
This will cause a compilation error:

```text
Error: Main method not found in class HelloWorld, please define the main method as:
public static void main(String[] args)
```

The program can’t start because the runtime can’t find the main() method in a non-static context.

3. **If void is omitted**:
   1.	The return type of the main() method is void, meaning it doesn’t return anything.
   2.	If you change it to something else, such as int or String, the Java runtime will expect the main() method to return that type, but it doesn’t, which will lead to a compilation error.
   3.	Example:
```java
public class HelloWorld {
    public static int main(String[] args) {  // Without void
        System.out.println("Hello, World!");
        return 0;
    }
}
```
This will result in a compilation error:
```text
Error: The main method must return a value of type void
```

4. **If String[] args is omitted:**
   1.	The parameter String[] args is used to capture command-line arguments.
   2.	While omitting this doesn’t cause a compilation error, it will mean that your program can’t accept any command-line arguments when it is run, which is totally fine in simple cases where no arguments are needed.
   3.	Example:
```java
public class HelloWorld {
    public static void main() {  // Without String[] args
        System.out.println("Hello, World!");
    }
}
```

This will compile and run, but you won’t be able to pass any arguments to the program. The args array is optional, and if not used, it will simply be ignored.

5. **What if we omit multiple parts (e.g., public, static, or void)?**
   1.	Omitting multiple parts in combination will typically result in a compilation error. For example, if you omit both public and static, the program will fail to run because the main() method would neither be accessible nor called properly.
   2.	Example:
```java
class HelloWorld {
    void main(String[] args) {  // Missing static and public
        System.out.println("Hello, World!");
    }
}
```
This will result in a compilation error:
```text
Error: Main method not found in class HelloWorld, please define the main method as:
public static void main(String[] args)
```

##  Variables & Constants
### Variables

Variables are containers that store data values. In Java, every variable must be declared with a **data type**.

```java
int age = 25;
String name = "World";
double price = 99.99;
boolean isActive = true;
```
You can change the value of a variable after it’s declared:
```java
age = 30;
```

### Constants

Constants are variables whose values cannot be changed after initialization. Use the final keyword to declare them.
```java
final int MAX = 100;
```
- Attempting to reassign MAX will cause a compile-time error.

## Data Types

### Primitive Data Types

These are the most basic types in Java, stored by value.

```text
| Type    | Size     | Example             |
|---------|----------|---------------------|
| int     | 4 bytes  | int x = 10;         |
| float   | 4 bytes  | float f = 5.5f;     |
| double  | 8 bytes  | double d = 5.5;     |
| char    | 2 bytes  | char c = 'A';       |
| boolean | 1 bit    | boolean b = true;   |
```
### Non-Primitive Data Types

These refer to objects and are stored by reference.
```text
| Type   | Description                          |
|--------|--------------------------------------|
| String | Sequence of characters (`"Hello"`)   |
| Array  | Collection of same-type elements     |
| Object | Instance of a class                  |
```
```java
String message = "Welcome!";
int[] numbers = {1, 2, 3};
MyClass obj = new MyClass();
```

## Operators

### Arithmetic Operators

Used for mathematical operations:
```text
| Operator | Description           | Example   |
|----------|-----------------------|-----------|
|  +       | Addition              |  a + b    |
|  -       | Subtraction           |  a - b    |
|  *       | Multiplication        |  a * b    |
|  /       | Division              |  a / b    |
|  %       | Modulus (remainder)   |  a % b    |
```
### Relational (Comparison) Operators

Used to compare two values:
```text
| Operator | Meaning            | Example   |
|----------|--------------------|-----------|
| ==       | Equal to           | a == b    |
| !=       | Not equal to       | a != b    |
| >        | Greater than       | a > b     |
| <        | Less than          | a < b     |
| >=       | Greater or equal   | a >= b    |
| <=       | Less or equal      | a <= b    |
```
### Logical Operators

Used to combine multiple conditions:
```text
| Operator | Description   | Example           |
|----------|---------------|-------------------|
| &&       | Logical AND   | (a > 0 && b < 10) |
| ||       | Logical OR    | (a > 0 || b < 10) |
| !        | Logical NOT   | !(a > 0)          |
```
## Conditional Statements

These control the flow of execution based on conditions.

### if Statement

Executes a block if the condition is true.
```java
if (age >= 18) {
    System.out.println("Adult");
}
```
### if-else Statement

Executes one block if the condition is true, another if false.

```java
if (score >= 50) {
    System.out.println("Passed");
} else {
    System.out.println("Failed");
}
```
### else-if Ladder

Tests multiple conditions in sequence.

```java
if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 75) {
    System.out.println("Grade B");
} else {
    System.out.println("Needs Improvement");
}
```
### switch Statement

Used when you have multiple possible values for a variable.

```java
int day = 2;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Another day");
}
```

## Loops in Java

Loops are used to execute a block of code repeatedly until a condition is met.

### for Loop

Used when you know in advance how many times to loop.

```java
for (int i = 0; i < 5; i++) {
    System.out.println("i = " + i);
}
```
- Initialization: int i = 0 → runs once
- Condition: i < 5 → checked before each iteration
- Increment: i++ → runs after each iteration

### while Loop

Used when the number of iterations is unknown and depends on a condition.

```java
int i = 0;
while (i < 5) {
    System.out.println("i = " + i);
    i++;
}
```
•	The loop runs only if the condition is true before entering.

### do-while Loop

Runs the loop at least once, then checks the condition.

```java
int i = 0;
do {
    System.out.println("i = " + i);
    i++;
} while (i < 5);
```
## Functions (Methods)

Functions in Java are called methods. They help break code into reusable blocks.

### Definition Syntax

```java
returnType methodName(parameters) {
    // code
    return value; // if returnType is not void
}
```
### Example with Return
```java
public int add(int a, int b) {
    return a + b;
}
```
### Example without Return

```java
public void greet(String name) {
    System.out.println("Hello, " + name);
}
```
### Calling a Method
```java
int sum = add(5, 3);        // returns 8
greet("World");          // prints: Hello, World
```

## Arrays in Java

Arrays are containers that hold multiple values of the same data type.

### 1D Arrays (Single-Dimensional)
```java
int[] nums = {10, 20, 30};
System.out.println(nums[0]); // prints 10

// Iterating
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}
```
- Array indices start from 0.
- s.length gives the size of the array.

### 2D Arrays (Matrix)
```java
int[][] matrix = {
    {1, 2},
    {3, 4}
};

System.out.println(matrix[0][1]); // prints 2

// Iterating
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

## Strings in Java

A String is a sequence of characters. Strings are immutable in Java.
```java
String name = "World";
System.out.println(name.length());     // 5
System.out.println(name.charAt(0));    // W
System.out.println(name.toUpperCase()); // WORLD
System.out.println(name.contains("rld")); // true
```
###  Common `String` Methods in Java
```text
| Method                | Description                              |
|-----------------------|------------------------------------------|
| length()              | Returns the number of characters         |
| charAt(index)         | Returns char at a given index            |
| toLowerCase()         | Converts to lowercase                    |
| toUpperCase()         | Converts to uppercase                    |
| substring(start, end) | Returns a part of the string             |
| equals(str)           | Checks if two strings are equal          |
| contains(str)         | Checks if string contains substring      |
```
### String Concatenation
```java
String fullName = "Hello" + "World";
System.out.println(fullName); // Hello World
```
