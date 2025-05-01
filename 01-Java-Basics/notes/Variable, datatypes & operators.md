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

✅ Next: [Conditional-Statements.md](Conditional-Statements.md)