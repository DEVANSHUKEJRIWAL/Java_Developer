# 🌿 Java 8+ Features in Depth

Java 8 introduced powerful features that brought functional programming and modern API enhancements to Java. These are essential for writing clean, concise, and efficient Java code.

---

## 🔹 1. Lambda Expressions

A **lambda** is an anonymous function that can be treated as a value and passed around.

###  Syntax:
```java
(parameters) -> { body }
```
### Example:
```java
Runnable r = () -> System.out.println("Running a lambda thread!");
r.run();
```
### With parameters:
```java
BiFunction<Integer, Integer, Integer> sum = (a, b) -> a + b;
System.out.println(sum.apply(5, 3)); // 8
```

## 2. Functional Interfaces

An interface with a single abstract method, used with lambdas.

### Custom Functional Interface:

```java
@FunctionalInterface
interface Greet {
    void say(String name);
}
Greet g = (name) -> System.out.println("Hello, " + name);
g.say("World");
```
### Common Built-in Interfaces (from java.util.function):
```text

| Interface      | Description                | Example                        |
|----------------|----------------------------|--------------------------------|
| Predicate<T>   | Returns boolean            | x -> x > 0                     |
| Consumer<T>    | Performs an action         | x -> System.out.println(x)     |
| Supplier<T>    | Provides a value           | () -> "Hello"                  |
| Function<T, R> | Transforms input to output | x -> x.toString()              |
```
## 3. Stream API

Streams allow processing collections in a declarative, chainable, and parallelizable way.

### Example: Filtering and Mapping
```java
List<String> names = Arrays.asList("World", "Ansh", "Ravi");

names.stream()
     .filter(n -> n.startsWith("W"))
     .map(String::toUpperCase)
     .forEach(System.out::println); // World
```
### Common Stream Methods
```text
| Method        | Description                          | Example                      |
|---------------|--------------------------------------|------------------------------|
| filter()      | Filters elements based on condition  | x -> x.length() > 3          |
| map()         | Transforms elements                  | String::toUpperCase          |
| sorted()      | Sorts stream elements                | Comparator.naturalOrder()    |
| collect()     | Collects into list/set/map           | Collectors.toList()          |
| count()       | Returns the count                    | stream.count()               |
| anyMatch()    | Returns true if any match condition  | x -> x.startsWith("A")       |
| reduce()      | Accumulates into one result          | (a, b) -> a + b              |
```
### Example: Sum using reduce
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4);
int sum = nums.stream().reduce(0, (a, b) -> a + b); // 10
```
## 4. Optional Class

Optional is a container to avoid null and prevent NullPointerException.

### Creating Optional:
```java
Optional<String> name = Optional.of("World");
System.out.println(name.get()); // World
```
### Common Methods:
-	isPresent()
-	ifPresent(Consumer)
-	orElse(defaultValue)
-	map(###

### Example:

```java
Optional<String> name = Optional.ofNullable(null);
System.out.println(name.orElse("Default")); // Default
```
## 5. Default and Static Methods in Interfaces

Interfaces can now have method implementations using default or static.

### Default Method:
```java
interface MyInterface {
    default void greet() {
        System.out.println("Hello from default method");
    }
}
```
### Static Method:
```java
interface Utility {
    static int square(int x) {
        return x * x;
    }
}
```
## 6. New Date & Time API (java.time package)

Replaces the outdated Date and Calendar classes with cleaner and immutable APIs.

### LocalDate, LocalTime, LocalDateTime
```java
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime dt = LocalDateTime.of(2025, Month.APRIL, 29, 18, 0);
```
### Formatting:
```java
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm");
System.out.println(dt.format(fmt));
```
### Duration and Period:
```java
Period p = Period.between(LocalDate.of(2020, 1, 1), LocalDate.now());
System.out.println(p.getYears()); // Difference in years
```
### Summary Table

```text
| Feature               | Description                         | Example                      |
|---------------------  |-------------------------------------|------------------------------|
| Lambda Expressions    | Anonymous functions                 | (x, y) -> x + y              |
| Functional Interfaces | Interface with 1 abstract method    | @FunctionalInterface         |
| Stream API            | Process collections functionally    | filter().map().collect()     |
| Optional              | Avoid null and NPE                  | Optional.ofNullable()        |
| Default Methods       | Method body in interface            | default void show()          |
| Static Methods        | Interface static utility methods    | static int sum()             |
| Date & Time API       | Modern time handling (immutable)    | LocalDate, Period            |
```
### Real-world Use Case
```java
List<Employee> emps = getEmployees();

Map<String, List<Employee>> grouped =
    emps.stream()
        .collect(Collectors.groupingBy(Employee::getDepartment));

grouped.forEach((dept, list) -> {
    System.out.println(dept + ": " + list.size());
});
```
🥳🥳Hurray! You've finished phase-2: Core-Java-OOP.
