# 🔌 JDBC and SQL with Java

JDBC (Java Database Connectivity) is a standard API that enables Java applications to connect and interact with relational databases like MySQL or PostgreSQL.

---

## ✅ What You’ll Learn

- How to connect Java code to a database
- CRUD operations using JDBC
- Key JDBC interfaces and classes
- Best practices

---

## 📦 JDBC Architecture

1. Load JDBC Driver
2. Establish `Connection`
3. Create `Statement` or `PreparedStatement`
4. Execute Query
5. Process `ResultSet`
6. Close all resources

---

## 🔧 Step-by-Step Setup with MySQL

### ✅ Add MySQL Dependency (Maven)
```xml
##xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>
```
### ✅ Full Example: Fetch User by ID
```java
import java.sql.*;

public class JDBCExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydb";
        String username = "root";
        String password = "your_password";

        try {
            // Step 1: Connect to DB
            Connection conn = DriverManager.getConnection(url, username, password);

            // Step 2: Prepare SQL
            String query = "SELECT * FROM users WHERE id = ?";
            PreparedStatement stmt = conn.prepareStatement(query);
            stmt.setInt(1, 1); // set parameter

            // Step 3: Execute
            ResultSet rs = stmt.executeQuery();

            // Step 4: Process result
            while (rs.next()) {
                System.out.println("User: " + rs.getString("username"));
            }

            // Step 5: Close
            rs.close();
            stmt.close();
            conn.close();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```
### 🧾 CRUD Operation Summary

```text
| Operation | SQL Syntax Example                                 |
|-----------|----------------------------------------------------|
| Create    | INSERT INTO users (name) VALUES ('Dev')            |
| Read      | SELECT * FROM users WHERE id = 1                   |
| Update    | UPDATE users SET name='Ansh' WHERE id = 1          |
| Delete    | DELETE FROM users WHERE id = 1                     |
```
### 🔑 Key JDBC Interfaces
```text
| Interface         | Purpose                                     |
|-------------------|---------------------------------------------|
| Connection        | Connects to the DB                          |
| PreparedStatement | Executes parameterized queries              |
| ResultSet         | Holds result data from SELECT queries       |
| DriverManager     | Gets a Connection from the JDBC driver      |

```

## ⚠️ Best Practices
-	Always close Connection, Statement, and ResultSet to avoid memory leaks.
-	Prefer PreparedStatement over Statement for security (avoids SQL injection).
-	Use try-with-resources for automatic cleanup.
```java
try (Connection conn = DriverManager.getConnection(...);
     PreparedStatement stmt = conn.prepareStatement(...)) {
     // use stmt
}
```
Link to Next-> Servlets-and-JSP.md
