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
🥳🥳Hurray! You've finished phase-1: Java-Basics.