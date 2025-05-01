# 🛠️ Tools for Backend Development

In this section, we’ll cover the key tools and technologies that complement your Spring Boot development, including **Maven/Gradle**, **MySQL/PostgreSQL**, **Postman**, and **Docker**.

---

## 🧠 Key Tools

### 🔹 Maven / Gradle

**Maven** and **Gradle** are build automation tools that manage dependencies, build your projects, and handle deployment.

#### ✅ Maven Example

1. **Add Dependencies (pom.xml)**
```xml
#xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

2.	Build and Run:
```text
mvn clean install
mvn spring-boot:run
```

✅ Gradle Example
1.	Add Dependencies (build.gradle)

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
}
```
2.	Build and Run:

```text
gradle build
gradle bootRun
```
```text
| Tool    | Description                                          |
|---------|------------------------------------------------------|
| Maven   | Dependency management and project build tool         |
| Gradle  | Faster alternative to Maven, flexible build system   |
```

## 🔹 MySQL / PostgreSQL

MySQL and PostgreSQL are the relational databases most commonly used with Spring Boot for data persistence.

### MySQL Example
#### 1.	Configure in application.properties:

```properties
## properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
```
#### 2.	Create Database (via MySQL CLI):

```sql
#sql
CREATE DATABASE mydb;
```
##  PostgreSQL Example
### 1.	Configure in application.properties:

```properties
#properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=postgres
spring.datasource.password=password
```
### 2.	Create Database (via PostgreSQL CLI):

```sql
#sql
CREATE DATABASE mydb;
```
## 🔹 Postman

Postman is a tool used for testing and debugging APIs. You can send GET, POST, PUT, DELETE requests and see the responses.

### Example – Testing a GET request:
1.	GET http://localhost:8080/books
2.	Check JSON response for the list of books.

## 🔹 Docker (Optional)

Docker allows you to containerize your Spring Boot application and make it portable across different environments.

##  Basic Dockerfile

```dockerfile
##dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/myapp.jar myapp.jar
ENTRYPOINT ["java", "-jar", "myapp.jar"]
```
### 1.	Build Docker Image:

```text
docker build -t myapp .
```
### 2.	Run Docker Container:

```text
docker run -p 8080:8080 myapp
```

## 📌 Tools Summary

```text
| Tool             | Description                              | Example Usage        |
|------------------|------------------------------------------|----------------------|
| Maven            | Build tool and dependency management     |  mvn clean install   |
| Gradle           | Faster build system                      |  gradle build        |
| MySQL/PostgreSQL | Relational databases for Spring Boot     | JDBC configuration   |
| Postman          | API testing tool                         | Test REST APIs       |
| Docker           | Containerize your Spring Boot app        |  docker build        |
```