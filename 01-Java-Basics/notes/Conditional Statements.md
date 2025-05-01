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
✅ Next: [Loops-Functions-Arrays.md](Loops-Functions-Arrays.md) 