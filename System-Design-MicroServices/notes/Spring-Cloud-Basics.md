# ☁️ Spring Cloud Basics

**Spring Cloud** is a collection of tools and libraries to build distributed systems and microservices. It adds support for service discovery, centralized configuration, fault tolerance, and routing.

---

## 🎯 Why Use Spring Cloud?

Spring Cloud simplifies:
- Inter-service communication
- Service registration/discovery
- Centralized configuration
- Load balancing
- Circuit breaking

---

## 🧱 Core Components

| Component          | Description                                     |
|--------------------|-------------------------------------------------|
| Eureka             | Service registry (Netflix OSS)                  |
| Spring Cloud Config| Centralized config for all microservices        |
| Zuul / Gateway     | API Gateway that routes requests                |
| Ribbon             | Client-side load balancing (Deprecated)         |
| Resilience4j       | Circuit breaker and fault tolerance             |

---

## 📘 1. Eureka Server (Service Registry)

### ✅ Setup Eureka Server
```java
@SpringBootApplication
@EnableEurekaServer
public class DiscoveryServerApp {
    public static void main(String[] args) {
        SpringApplication.run(DiscoveryServerApp.class, args);
    }
}
```
### ✅ Add to application.properties

```properties
##properties
server.port=8761
spring.application.name=discovery-server
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```
## 📘 2. Eureka Client

Used by microservices to register themselves with Eureka.

```java
@SpringBootApplication
@EnableEurekaClient
public class UserServiceApp { ... }
```
```properties
##properties
spring.application.name=user-service
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```
## 📘 3. Spring Cloud Gateway

Modern API gateway to route requests to backend services.

```java
@SpringBootApplication
public class ApiGatewayApp { ... }
```
```yaml
##yaml
spring:
  cloud:
    gateway:
      routes:
        - id: user-service
          uri: lb://user-service
          predicates:
            - Path=/users/**
```
✅ Load balancing is automatically handled with Eureka + Gateway.

### 🔁 Centralized Config with Spring Cloud Config
1.	Set up a Git repo for your application.yml configs.
2.	Use Spring Cloud Config Server to serve configs to all services.
```java
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApp { ... }
```
```properties
##properties
spring.cloud.config.server.git.uri=https://github.com/your/config-repo
```
✅ This avoids maintaining separate config files across services.

## 🔒 Resilience4j (Circuit Breaker)

Prevents cascading failures across services when one goes down.
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallbackUser")
public User getUserDetails() {
    return restTemplate.getForObject("http://user-service/users/1", User.class);
}
```
📌 Summary Table
```text
| Feature           | Tool                  | Purpose                                  |
|-------------------|-----------------------|------------------------------------------|
| Service Discovery | Eureka                | Auto-register and find services          |
| Routing           | Spring Cloud Gateway  | Forward traffic based on URL paths       |
| Centralized Config| Spring Cloud Config   | Single source of truth for config        |
| Fault Tolerance   | Resilience4j          | Retry, fallback, circuit breaking        |
```


