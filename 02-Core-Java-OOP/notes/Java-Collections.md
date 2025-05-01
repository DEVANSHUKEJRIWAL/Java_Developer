# 📦 Java Collections Framework (JCF)

Java Collections Framework provides a unified architecture to store, retrieve, and manipulate groups of data efficiently.

---

##  Categories of Collections

| Category | Interfaces              | Common Implementations                       |
|----------|-------------------------|----------------------------------------------|
| List     | `List<E>`               | `ArrayList`, `LinkedList`, `Vector`, `Stack` |
| Set      | `Set<E>`                | `HashSet`, `LinkedHashSet`, `TreeSet`        |
| Queue    | `Queue<E>`              | `PriorityQueue`, `ArrayDeque`, `LinkedList`  |
| Map      | `Map<K, V>`             | `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable` |

---

##  List

Ordered collection that allows duplicates. You can access elements by index.

##  `ArrayList`

```java
List<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
System.out.println(names.get(0)); // Alice
```
- Use when: Frequent reads and random access.

- Avoid when: Frequent inserts/removals in the middle (shifting is costly).

## `LinkedList`

Doubly-linked list. Slower access but better for frequent inserts/removals.

```java
LinkedList<String> list = new LinkedList<>();
list.add("Monday");
list.addFirst("Sunday");
list.removeLast(); // Removes "Monday"
```
- Use when: Frequent insertions/deletions at head or tail.

## `Set`

Unordered collection that doesn’t allow duplicates.

### HashSet
```java
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("A"); // Ignored, duplicate
```
- Use when: You want unique elements and don’t care about order.

### TreeSet

Sorted set based on natural ordering or a comparator.
```java
Set<Integer> sorted = new TreeSet<>();
sorted.add(3);
sorted.add(1);
System.out.println(sorted); // [1, 3]
```
- Use when: You need sorted unique elements.

## `Map`

Stores data as key-value pairs.

### HashMap
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("John", 90);
scores.put("Jane", 85);
System.out.println(scores.get("John")); // 90
```
- Use when: Fast lookup/insertion/deletion based on key.

### LinkedHashMap

Maintains insertion order of keys.
```java
Map<String, String> capital = new LinkedHashMap<>();
capital.put("India", "New Delhi");
capital.put("USA", "Washington");
System.out.println(capital); // Maintains order
```
### TreeMap

Sorted by keys (natural or custom comparator).
```java
Map<Integer, String> map = new TreeMap<>();
map.put(2, "B");
map.put(1, "A");
System.out.println(map); // {1=A, 2=B}
```
- Use when: You want sorted keys.

### Edge Cases & Best Practices
```text
| Topic                | Edge Case / Warning                                                                                       |
|----------------------|-----------------------------------------------------------------------------------------------------------|
| HashMap              | Allows one null key and many null values                                                                  |
| HashSet              | Relies on equals() and hashCode() — override them for custom objects                                      |
| Concurrent Access    | Regular collections are not thread-safe — use ConcurrentHashMap, Collections.synchronizedList() if needed |
| Iterating & Removing | Don’t remove elements in a regular for loop — use Iterator or removeIf()                                  |

```
### Real-world Example: Student Record System
```java
Map<String, List<Integer>> studentMarks = new HashMap<>();

studentMarks.put("Alice", Arrays.asList(90, 85, 88));
studentMarks.put("Bob", Arrays.asList(70, 60, 75));

for (Map.Entry<String, List<Integer>> entry : studentMarks.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```
