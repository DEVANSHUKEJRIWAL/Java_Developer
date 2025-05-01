# 📚 JPA + Hibernate – Object-Relational Mapping (ORM)

**JPA (Java Persistence API)** is a specification for ORM (Object-Relational Mapping) in Java. **Hibernate** is the most popular implementation of JPA. It allows Java objects to be mapped to database tables.

---

## 🧠 What is JPA?

JPA provides a standard interface for **mapping Java objects to relational database tables**. It simplifies database interactions by abstracting the complexities of SQL.

---

## 🛠 Hibernate Annotations

### ✅ `@Entity`: Marks a class as a database entity
```java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    // Getters, Setters
}
```
```text
| Annotation        | Description                            |
|-------------------|----------------------------------------|
|  @Entity          | Marks class as an entity               |
|  @Id              | Marks the primary key                  |
|  @GeneratedValue  | Auto-generates the primary key value   |
|  @Column          | Customizes column properties           |
```

## 🔄 @ManyToOne, @OneToMany, @ManyToMany

### ✅ One-to-Many Relationship Example
```java
@Entity
public class Author {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "author")
    private List<Book> books;
}

@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToOne
    @JoinColumn(name = "author_id")
    private Author author;
}
```
## 🛠 JPA Repositories

JPA repositories simplify the data access layer. You can easily perform CRUD operations without writing boilerplate code.
```java
public interface BookRepository extends JpaRepository<Book, Long> {
    List<Book> findByTitle(String title);
}
```
```text 
| Method        | Description                        |
|---------------|------------------------------------|
|  findById()   | Find an entity by ID               |
|  findAll()    | Get all entities                   |
|  save()       | Save or update an entity           |
|  deleteById() | Delete an entity by ID             |

```
### 🧪 Example: CRUD Operations

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @Autowired
    private BookRepository bookRepo;

    // Create
    @PostMapping
    public Book createBook(@RequestBody Book book) {
        return bookRepo.save(book);
    }

    // Read
    @GetMapping("/{id}")
    public Book getBook(@PathVariable Long id) {
        return bookRepo.findById(id).orElseThrow();
    }

    // Update
    @PutMapping("/{id}")
    public Book updateBook(@PathVariable Long id, @RequestBody Book book) {
        Book existingBook = bookRepo.findById(id).orElseThrow();
        existingBook.setTitle(book.getTitle());
        return bookRepo.save(existingBook);
    }

    // Delete
    @DeleteMapping("/{id}")
    public void deleteBook(@PathVariable Long id) {
        bookRepo.deleteById(id);
    }
}
```
### 📝 Hibernate and JPA Best Practices
```text
| Practice                                       | Description                                           |
|------------------------------------------------|-------------------------------------------------------|
| Avoid N+1 query problem                        | Use  @ManyToOne(fetch = FetchType.LAZY)               |
| Use  @Transactional  for multi-step operations | Ensure operations are wrapped in a single transaction |
| Always check for  Optional  in repositories    | Prevent  NullPointerException                         |
```

