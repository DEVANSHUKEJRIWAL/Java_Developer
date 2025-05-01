#  Syntax & Structure
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
✅ Next: [Variables-DataTypes-Operators.md](Variables-DataTypes-Operators.md) 