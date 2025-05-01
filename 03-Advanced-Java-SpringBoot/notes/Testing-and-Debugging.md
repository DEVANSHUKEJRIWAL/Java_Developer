# 🧪 Testing & Debugging in Spring Boot

Testing is crucial for ensuring your Spring Boot applications are reliable and bug-free. In this section, we’ll focus on **unit testing** with JUnit 5, mocking dependencies with **Mockito**, and using **Postman** for API testing.

---

## 🧠 JUnit 5 – Unit Testing

JUnit 5 is the most widely used testing framework for Java applications. It helps write automated tests to verify your logic.

###  JUnit 5 Test Example

```java
@SpringBootTest // Bootstraps Spring context for testing
class BookServiceTest {
    
    @Autowired
    private BookService bookService; // Service class we want to test
    
    @Test
    void testSaveBook() {
        // Test book creation
        Book book = new Book("Test Book");
        Book savedBook = bookService.save(book);
        assertNotNull(savedBook);
        assertEquals("Test Book", savedBook.getTitle());
    }
}
```
###  Common Annotations
```text
| Annotation       | Description                                           |
|------------------|-------------------------------------------------------|
|  @Test           | Marks the method as a test method                     |
|  @BeforeEach     | Setup before each test method                         |
|  @AfterEach      | Cleanup after each test method                        |
|  @SpringBootTest | Loads the full Spring context for integration tests   |
```

##🧪 Mockito – Mocking Dependencies

Mockito allows you to mock service dependencies for testing without relying on the actual implementations (like databases).

### Mockito Example
```java
@ExtendWith(MockitoExtension.class) // Run tests with Mockito
class BookControllerTest {

    @Mock
    private BookService bookService; // Mocked service
    
    @InjectMocks
    private BookController bookController; // Inject mocks into controller
    
    @Test
    void testGetAllBooks() {
        // Setup mock behavior
        when(bookService.getAll()).thenReturn(List.of(new Book("Test Book")));
        
        // Call the controller method
        List<Book> books = bookController.getAll();
        
        // Verify results
        assertEquals(1, books.size());
        assertEquals("Test Book", books.get(0).getTitle());
    }
}
```

### Common Mockito Methods
```text
Method
Description
@Mock
Creates a mock object
@InjectMocks
Injects mocks into the class under test
when(...).thenReturn(...)
Specifies behavior for mocked methods

```

## 🧪 Postman – API Testing

Postman is a powerful tool for testing REST APIs. It allows you to send different types of HTTP requests (GET, POST, PUT, DELETE) and view responses.

###  Postman Test Example
1.	Send a GET request to http://localhost:8080/books
2.	View JSON Response for list of books

	•	POST Request:
	•	Body: {"title": "New Book"}
	•	URL: http://localhost:8080/books

###  Common Postman Features
```text
| Feature | Description                                       |
|---------|---------------------------------------------------|
| Headers | Set HTTP headers (e.g., Content-Type)             |
| Body    | Set request body for POST/PUT requests            |
| Tests   | Write assertions to validate responses            | 
```

## 🧑‍🔧 Debugging in Spring Boot

Debugging is critical to identify issues in your application.

### ✅ Common Debugging Techniques
-	Use @Slf4j (Lombok) or Logger to log important information.
```java
@Slf4j
@Service
public class BookService {
    public Book save(Book book) {
        log.info("Saving book: {}", book.getTitle());
        return bookRepository.save(book);
    }
}
```
-	Use Breakpoints in IDE (IntelliJ IDEA, Eclipse) to inspect variable states and flow.

## 📌 Summary Table
```text
| Tool/Concept | Description                          | Example                            |
|--------------|--------------------------------------|------------------------------------|
| JUnit 5      | Testing framework for unit tests     |  @Test  method                     |
| Mockito      | Mocking service dependencies         |  @Mock ,  when(...).thenReturn(...)|
| Postman      | Tool for testing APIs                | Sending HTTP requests              |
| Logging      | Add logs for debugging               |  log.info("Message")               |

```

✅  Next: [Tools (Maven, Postman, Docker)](Tools.md)