# ⚙️ Redis & RabbitMQ (Optional but Powerful)

These tools aren’t mandatory for beginner microservices but are widely used in **real-world systems** for performance, reliability, and scalability.

---

## 🔹 Redis – In-Memory Data Store

**Redis** is a key-value NoSQL store used for:
- Caching
- Session storage
- Real-time data access
- Distributed locking

---

### ✅ Why Use Redis?

| Use Case            | Description                                   |
|---------------------|-----------------------------------------------|
| Caching             | Reduce DB calls for frequently accessed data  |
| Session Management  | Store logged-in user sessions                 |
| Rate Limiting       | Count requests per IP in Redis                |
| Pub/Sub             | Message broadcasting                          |

---

### ✅ Example: Using Redis with Spring Boot

#### 1. Add Redis Dependency (Maven)
```xml
#xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
### 2. Configure Redis in application.properties

```properties
#properties
spring.redis.host=localhost
spring.redis.port=6379
```

### 3. Use RedisTemplate
```java
@Service
public class CacheService {
    @Autowired
    private RedisTemplate<String, String> redisTemplate;

    public void save(String key, String value) {
        redisTemplate.opsForValue().set(key, value);
    }

    public String get(String key) {
        return redisTemplate.opsForValue().get(key);
    }
}
```
- **Redis runs locally or in Docker: docker run -p 6379:6379 redis**

## 🔹 RabbitMQ – Message Broker

RabbitMQ helps services communicate asynchronously via messages. It’s useful for:
-	Decoupling services
-	Background jobs
-	Reliable delivery
-	Event-driven systems

### 🧠 Example Use Case
```text
| Service       | Event              | Action                         |
|---------------|--------------------|--------------------------------|
| OrderService  | Order placed       | Sends message to EmailService  |
| EmailService  | Listens to message | Sends confirmation email       |
```

##  RabbitMQ Spring Boot Setup

### 1. Add RabbitMQ Dependency
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

### 2. Configuration
```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
```
### 3. Publisher
```java
@Autowired
private AmqpTemplate amqpTemplate;

public void send(String message) {
    amqpTemplate.convertAndSend("order-exchange", "order.key", message);
}
```
### 4. Listener
```java
@RabbitListener(queues = "order-queue")
public void listen(String message) {
    System.out.println("Received: " + message);
}
```
###  Run RabbitMQ in Docker:
```text
docker run -p 5672:5672 -p 15672:15672 rabbitmq:management
```
### ⚖️ Redis vs RabbitMQ Summary
```text
| Tool      | Type             | Use Case                          |
|-----------|------------------|-----------------------------------|
| Redis     | In-memory DB     | Caching, real-time access         |
| RabbitMQ  | Message broker   | Async communication, decoupling   |

```

### ✅ When Should You Learn These?
```text
| Scenario                        | Recommendation              |
|---------------------------------|-----------------------------|
| Simple REST APIs                | ❌ Not required             |
| High scale or async tasks       | ✅ Use Redis/RabbitMQ       |
| Learning advanced microservices | ✅ Great to explore         |
```

