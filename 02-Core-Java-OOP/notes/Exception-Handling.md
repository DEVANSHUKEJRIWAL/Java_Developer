# ❗ Exception Handling in Java

Exception Handling allows you to gracefully handle runtime errors and maintain the normal flow of the application.

---

##  What is an Exception?

An **exception** is an event that disrupts the normal flow of a program. It is an object that is thrown at runtime when an error occurs.

Java provides a robust **try-catch-finally** mechanism to handle exceptions.

---

##  Types of Exceptions

| Type                 | Description                                    | Examples                          |
|----------------------|------------------------------------------------|-----------------------------------|
| **Checked**          | Must be handled at compile-time                | `IOException`, `SQLException`     |
| **Unchecked**        | Occur at runtime, not required to handle       | `NullPointerException`, `ArithmeticException` |
| **Errors** (rare)    | Serious issues, not meant to be caught         | `OutOfMemoryError`, `StackOverflowError` |

---

##  try-catch Block

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
}
```
- Catch block is used to handle specific exceptions.

## Multiple catch Blocks
```java
try {
    String text = null;
    System.out.println(text.length());
} catch (NullPointerException e) {
    System.out.println("Null value!");
} catch (Exception e) {
    System.out.println("Something went wrong.");
}
```
- Always catch more specific exceptions before generic ones (Exception).

## finally Block

The finally block is always executed whether an exception occurs or not.
```java
try {
    int[] arr = new int[3];
    arr[4] = 5;
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Index error!");
} finally {
    System.out.println("Cleanup done.");
}
```
## throw Keyword

Used to explicitly throw an exception.
```java
throw new IllegalArgumentException("Age must be 18+");
```
- Used for validation inside methods.

## throws Keyword

Used to declare exceptions a method might throw.
```java
public void readFile() throws IOException {
    FileReader file = new FileReader("data.txt");
}

```

- You must handle it in the calling method or declare further.

## Custom Exceptions

You can define your own exception class by extending Exception or RuntimeException.
```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public void validateAge(int age) throws InvalidAgeException {
    if (age < 18) throw new InvalidAgeException("Underage!");
}

```
## Edge Cases & Pitfalls
```text
| Case                              | Notes                                                            |
|-----------------------------------|------------------------------------------------------------------|
| catch (Exception e) first         |  Will block more specific exceptions from being caught properly  |
| Empty catch block                 |  Avoid swallowing exceptions silently                            |
| Returning from finally block      |  Avoid — it overrides any return in try or catch                 |
| Using exceptions for flow control |  Very bad practice — use logic instead                           |
```
## Real-world Example: Bank Withdrawal
```java
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String msg) {
        super(msg);
    }
}

public class Bank {
    private int balance = 500;

    public void withdraw(int amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException("Not enough balance");
        }
        balance -= amount;
        System.out.println("Withdrawn: " + amount);
    }
}
```
###  Best Practices
-	Catch only those exceptions you can handle meaningfully.
-	Log exceptions for debugging (using e.printStackTrace() or logging frameworks).
-	Use custom exceptions for business logic clarity.
-	Always clean up resources (finally, try-with-resources).

## Summary
```text
| Concept | Purpose                             | Example / Keyword              |
|---------|-------------------------------------|--------------------------------|
| try     | Code that may throw an exception    | try { riskyCode(); }           |
| catch   | Handle the thrown exception         | catch (IOException e)          |
| finally | Execute regardless of exception     | Close resources, logs          |
| throw   | Manually raise an exception         | throw new IllegalArg()         |
| throws  | Declare method might throw exception| throws IOException             |
```

