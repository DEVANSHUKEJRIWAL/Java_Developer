# 🌱 Spring Framework – Core Concepts

Spring Framework is the backbone of Spring Boot. It provides powerful features like **Inversion of Control (IoC)** and **Dependency Injection (DI)**, which simplify large-scale Java development.

---

## 🧠 Core Concepts

### 🔸 Inversion of Control (IoC)
IoC means **the framework creates and manages your objects**, not you. You just define what should happen, and Spring handles the "how".

### 🔸 Dependency Injection (DI)
DI means you don’t create objects manually — Spring **injects** them into your classes.

---

## ✅ Why Use IoC and DI?

| Without Spring                          | With Spring Framework             |
|----------------------------------------|----------------------------------|
| You manage object creation manually    | Spring creates objects (beans)   |
| Tight coupling between classes         | Loose coupling via interfaces    |
| Hard to test and maintain              | Testable and modular code        |

---

## 🧪 Example with Comments

```java
// Service Layer
@Component
public class EmailService {
    public void sendEmail(String user) {
        System.out.println("Email sent to " + user);
    }
}

// Controller Layer
@RestController
public class UserController {

    private final EmailService emailService;

    // Constructor-based Dependency Injection
    public UserController(EmailService emailService) {
        this.emailService = emailService;
    }

    @GetMapping("/send")
    public String send() {
        emailService.sendEmail("dev@example.com");
        return "Sent!";
    }
}
```

## 🧾 Core Annotations

```text
| Annotation         | Description                                      |
|--------------------|--------------------------------------------------|
|  @Component        | Marks a class as a Spring Bean                   |
|  @Service          | Specialization of  @Component  for services      |
|  @Repository       | Specialization for data access layer             |
|  @Controller       | Handles web requests (for MVC apps)              |
|  @RestController   | Combines  @Controller  +  @ResponseBody          |
|  @Autowired        | Tells Spring to inject a bean automatically      |

```

## 🧰 Constructor vs Field Injection

###  Constructor injection is recommended — ensures all required dependencies are present when the object is created.

 Field injection works, but it’s harder to test and mock.
```java
//  Good
public MyController(MyService service) {
    this.service = service;
}

//  Avoid
@Autowired
private MyService service;
```

##  📌 Spring Core Summary Table
```text
| Concept               | Meaning                                          |
|-----------------------|--------------------------------------------------|
| IoC                   | Spring manages the lifecycle of your beans       |
| DI                    | Dependencies are injected automatically          |
|  @Component           | Declares a class as a managed Spring bean        |
|  @Autowired           | Automatically wires dependencies                 |
| Constructor Injection | Most recommended DI method                       |

```
