# 🔤 String Handling in Java

A **String** in Java is an object that represents a sequence of characters. Strings are widely used in Java programs and are **immutable**, meaning their values cannot be changed once created.

---

## 📌 1. Creating Strings

You can create strings in two ways:

```java
String s1 = "Hello";                   // String literal (recommended)
String s2 = new String("Hello");       // Using constructor
```

```text
| Creation Type    | Description              | Memory              |
|------------------|--------------------------|---------------------|
| String Literal   | Stored in String Pool    | Efficient           |
| new String()     | Stored in Heap memory    | Avoid if possible   |
```

🔹 What is the String Pool?
-	The String Pool (also called intern pool) is a special memory area inside the heap where Java stores string literals.
-   It is used to optimize memory by reusing immutable string objects.
 
## 🧠 2. Why Are Strings Immutable?
-	 **Security:** Used in class loading, networking, etc.
-	 **Thread Safety:** No risk of accidental change.
-	 **Caching:** JVM can reuse String literals.
-	 **Hashcode Stability:** Required for using Strings as map keys.


### 🛠️ 3.  Common `String` Methods in Java
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
| trim()                | Removes leading/trailing whitespaces     |
| replace(a, b)         | Replaces characters                      |
```
### ➕ 4. String Concatenation

####  Using + Operator
```java
String fullName = "Hello" + "World";
System.out.println(fullName); // Hello World
```

####  Using concat()
```java
String msg = "Java".concat(" Developer");
System.out.println(msg); // Java Developer
```

### 🔁 5. Comparing Strings
```java
String a = "hello";
String b = new String("hello");

System.out.println(a == b);         // false (compares references)
System.out.println(a.equals(b));    // true  (compares values)
```

```text
| Operator   | Compares             | Result                                   |
|------------|----------------------|------------------------------------------|
| `==`       | Memory references    | May be false even if strings match       |
| `equals()` | Actual content/values| Preferred for comparison                 |
```

### 🧪 6. Edge Cases
```text
| Case                           | Result or Behavior                          |
|--------------------------------|---------------------------------------------|
| `charAt()` with invalid index  | Throws `StringIndexOutOfBoundsException`    |
| `null.equals("text")`          | Throws `NullPointerException`               |
| `"text".equals(null)`          | Returns `false`                             |
| `""` (empty string) vs `null`  | `""` is a valid object; `null` is not       |
```
## 🚀 7. Performance with StringBuilder & StringBuffer

### 🔸 Why not use + in loops?

```java
// Bad (creates many intermediate strings)
String result = "";
for (int i = 0; i < 5; i++) {
    result += i;
}
```
🔁 **Creates multiple intermediate objects and is slow.**

###  Use StringBuilder (Fast & Not Thread-Safe)
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb); // Hello World
```
###  Use StringBuffer (Thread-Safe Alternative)
```java
StringBuffer buffer = new StringBuffer("Java");
buffer.append(" Developer");
System.out.println(buffer); // Java Developer
```
*Note*:- We will cover about **thread-safety** in the upcoming phase.

### 🔄 8. String vs StringBuilder vs StringBuffer
```text
| Type          | Mutable | Thread-Safe| Use Case                                  |
|---------------|---------|------------|-------------------------------------------|
| String        |   No    |   Yes      | Fixed/constant strings, safe by default   |
| StringBuilder |   Yes   |   No       | Best for loops and fast concatenation     |
| StringBuffer  |   Yes   |   Yes      | Used in multi-threaded environments       |

```
🎉 **Congratulations!**

You’ve now completed the final topic of Phase 1: Java Basics.
