# 📂 File Handling in Java

File handling enables Java applications to read from and write to text files or binary files. Java uses I/O (Input/Output) streams for file operations.

---

##  Reading a File: FileReader & BufferedReader

```java
try {
    FileReader fr = new FileReader("input.txt");
    BufferedReader br = new BufferedReader(fr);
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
    br.close();
} catch (IOException e) {
    e.printStackTrace();
}
```
- Use BufferedReader for efficient line-by-line reading.

### Writing to a File: FileWriter
```java
try {
    FileWriter fw = new FileWriter("output.txt", true); // true for append
    fw.write("Hello, World!\n");
    fw.close();
} catch (IOException e) {
    e.printStackTrace();
}
```
- Always close the writer to save changes and free resources.

### Object Serialization

Serialization = converting an object into a byte stream for storage or transmission.

- Writing an Object to a File
```java
class Student implements Serializable {
    String name;
    int age;
}
```
```java
Student s = new Student("Dev", 22);
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("student.ser"));
out.writeObject(s);
out.close();
```
- Reading an Object
```java
ObjectInputStream in = new ObjectInputStream(new FileInputStream("student.ser"));
Student s = (Student) in.readObject();
in.close();
```
### Notes:
-	Class must implement Serializable.
-	transient fields are skipped during serialization.
-	Class versioning matters (use serialVersionUID).

- File handling is essential in logging, data persistence, and simple database emulation.
###

✅ Next: [Java 8+ Features (Streams, Lambdas, Functional Interfaces)](Java8_Features.md)
