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
✅ Next: [String-Handling.md](String-Handling.md) 