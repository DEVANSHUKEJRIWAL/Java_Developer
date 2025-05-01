# 📊 Logging & Monitoring in Microservices

In a distributed microservice system, it's essential to:
- Trace issues across services
- Monitor service health and performance
- Analyze logs centrally

This section introduces tools like **Log4j**, **Prometheus**, and **Grafana**.

---

## 🔹 Logging with Log4j / SLF4J

Spring Boot uses **SLF4J** + **Logback** by default, but you can also integrate Log4j.

###  Logging Levels

| Level     | Purpose                          |
|-----------|----------------------------------|
| `TRACE`   | Very detailed (rarely used)      |
| `DEBUG`   | Debugging info                   |
| `INFO`    | Standard logs                    |
| `WARN`    | Something might be wrong         |
| `ERROR`   | Something definitely went wrong  |

###  Example: Logging in Spring Boot
```java
@Slf4j // Lombok annotation
@Service
public class OrderService {

    public void placeOrder() {
        log.info("Placing order...");
        log.debug("Order payload validated");
        log.error("Failed to process order"); // Only if something breaks
    }
}
```
###  Configuring Log Levels (application.properties)

```properties
#properties
logging.level.root=INFO
logging.level.com.myapp=DEBUG
logging.file.name=logs/app.log
```

## 🔹 Monitoring with Prometheus + Grafana

### 🧠 Prometheus

An open-source tool that scrapes metrics from your application and stores time-series data.

### 🧠 Grafana

A visualization tool that connects to Prometheus and displays real-time dashboards.

###  Setup Monitoring in Spring Boot

#### 1. Add Actuator + Micrometer
```xml
##xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```
#### 2. application.properties
```properties
##properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
management.metrics.export.prometheus.enabled=true
```

#### 3. Prometheus scrapes metrics at:
```text
http://localhost:8080/actuator/prometheus
```

###  Docker Compose for Prometheus + Grafana
```yaml
##yaml
version: '3'
services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
```

### ➡️ Access:
- Prometheus UI: [http://localhost:9090](http://localhost:9090)
- Grafana Dashboard: [http://localhost:3000](http://localhost:3000) (default login: `admin` / `admin`)

---

## 📈 Sample Prometheus Configuration (`prometheus.yml`)

```yaml
##yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: 'spring-boot-app'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['host.docker.internal:8080']
```
- **host.docker.internal lets Docker access services running on your machine (for Mac/Windows).**

## 📌 Summary Table
```text
| Tool             | Purpose                          | Used For                                    |
|------------------|----------------------------------|---------------------------------------------|
| Log4j / SLF4J    | Logging system                   | Track events, errors, app flow              |
| Actuator         | Exposes health and metrics       | Expose endpoints like `/health`, `/metrics` |
| Prometheus       | Time-series metrics collection   | Monitors service CPU, memory, uptime        |
| Grafana          | Visualization dashboard          | Create real-time charts and alerts          |
```
##  Best Practices
```text
| Practice                        | Why It Helps                                 |
|---------------------------------|----------------------------------------------|
| Use `@Slf4j` or `LoggerFactory` | Avoids `System.out.println()` clutter        |
| Log errors with context         | Easier debugging (include order/user IDs)    |
| Avoid excessive logging         | Reduces log size, improves performance       |
| Use centralized log system      | Combine logs across all microservices        |
```
✅ Next: [Docker & Kubernetes](notes/Docker-and-Kubernetes.md)
