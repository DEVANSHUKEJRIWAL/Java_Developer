# ⚡ Spring Boot – Rapid Backend Development

Spring Boot is built on top of the Spring Framework and makes backend development fast, simple, and production-ready. It auto-configures your application, embeds a server (like Tomcat), and lets you focus on writing logic.

---

## 🧠 Why Spring Boot?

| Feature                  | Benefit                                     |
|--------------------------|---------------------------------------------|
| Embedded Tomcat          | No need to deploy WAR files                 |
| Auto-configuration       | Zero manual config for many use cases       |
| `application.properties` | Central config for ports, DB, etc.          |
| REST API ready           | Quickly expose endpoints with annotations   |

---

## 🚀 Starting Point

### ✅ Main Application Class
```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args); // Starts embedded server
    }
}
```
- 	**@SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan**

### 📦 Core Annotations


```text
| Annotation               | Purpose                                       |
|--------------------------|-----------------------------------------------|
|  @SpringBootApplication  | Main entry point for boot app                 |
|  @RestController         | Marks class as a REST API controller          |
|  @Service                | Used for business logic layer                 |
|  @Repository             | Data Access Layer (DB interaction)            |
|  @RequestMapping         | Base path for all endpoints in the controller |

```
## 🌐 RESTful API – CRUD Example

###  Sample Controller
```java
@RestController
@RequestMapping("/books")
public class BookController {

    @Autowired
    private BookRepository bookRepo;

    // GET: All books
    @GetMapping
    public List<Book> getAll() {
        return bookRepo.findAll();
    }

    // POST: Add book
    @PostMapping
    public Book create(@RequestBody Book book) {
        return bookRepo.save(book);
    }

    // PUT: Update book
    @PutMapping("/{id}")
    public Book update(@PathVariable Long id, @RequestBody Book book) {
        Book b = bookRepo.findById(id).orElseThrow();
        b.setTitle(book.getTitle());
        return bookRepo.save(b);
    }

    // DELETE: Remove book
    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id) {
        bookRepo.deleteById(id);
    }
}
```
### 🛠 application.properties

Used to set config values like server port, DB URL, Hibernate strategy, etc.
```java
server.port=8081

spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```

## 🔍 Swagger (Optional)

Swagger generates interactive documentation for your REST APIs.

###  Add Dependency (Gradle)
```groovy
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2'
```
###  Access the UI
-	Run the application
-	Visit: http://localhost:8080/swagger-ui.html

## 📌 HTTP Method Summary

```text
| Method  | Purpose             | Spring Annotation |
|---------|---------------------|-------------------|
| GET     | Read data           |  @GetMapping      |
| POST    | Create new resource |  @PostMapping     |
| PUT     | Update existing     |  @PutMapping      |
| DELETE  | Remove resource     |  @DeleteMapping   |
```
