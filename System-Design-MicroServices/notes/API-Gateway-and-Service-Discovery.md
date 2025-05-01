# 🌐 API Gateway & Service Discovery in Microservices

In a microservices architecture, we often need a way to:
- Register services dynamically
- Discover services without hardcoding URLs
- Route external requests to internal services

This is where **Service Discovery** and **API Gateways** help.

---

## 🔹 1. What is Service Discovery?

A mechanism that allows microservices to find each other **without hardcoded IPs/ports**.

###  Example:
- `UserService` registers itself with **Eureka Server**
- `OrderService` discovers `UserService` via Eureka

---

## 📦 Eureka Server (Netflix OSS)

Eureka is a registry where services register themselves and discover others.

###  Setup (Maven Dependency)
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```
###  Main Class
```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApp {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApp.class, args);
    }
}
```
###  Properties (application.yml)
```yaml
server:
  port: 8761
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

## 🧩 Eureka Client

Each microservice becomes a client to the Eureka server.

### Client Dependency
```xml
##xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
### Enable Client
```java
@SpringBootApplication
@EnableEurekaClient
public class ProductServiceApp { ... }
```

```yaml
##yaml
spring:
  application:
    name: product-service
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

## 🔹 2. What is an API Gateway?

An API Gateway is a single entry point for all client requests. It routes traffic to the appropriate microservice and can:
-	Handle authentication
-	Perform rate limiting
-	Transform requests/responses
-	Log traffic

## 📦 Spring Cloud Gateway (modern)

A modern replacement for Netflix Zuul (now deprecated).

### Add Dependency
```xml
##xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

### Configuration (application.yml)
```yaml
##yaml
spring:
  application:
    name: api-gateway
  cloud:
    gateway:
      routes:
        - id: user-service
          uri: lb://user-service
          predicates:
            - Path=/users/**
        - id: order-service
          uri: lb://order-service
          predicates:
            - Path=/orders/**
```
🔁 **lb:// tells the gateway to load balance using Eureka.**

## Gateway + Eureka Summary Table
```text
| Component        | Role                                             |
|------------------|--------------------------------------------------|
| Eureka Server    | Service registry                                 |
| Eureka Client    | Registers itself and discovers others            |
| Spring Gateway   | Routes requests based on path and service name   |
| `lb://` URI      | Uses service name for load balancing             |

```

### 🎯 Real-World Flow
1.	A user hits api-gateway.com/users/1
2.	Gateway matches /users/** and routes it to user-service
3.	user-service is discovered via Eureka

##  Benefits of This Setup
```text
| Feature             | Benefit                                      |
|---------------------|----------------------------------------------|
| Centralized Routing | All requests go through the API Gateway      |
| Dynamic Discovery   | No hardcoding service URLs                   |
| Load Balancing      | Works out-of-the-box with Eureka             |
| Easier Monitoring   | Gateway can track all API requests           |
```
