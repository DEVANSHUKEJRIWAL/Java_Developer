# 🌐 Servlets & JSP (Optional Fundamentals)

Although Spring Boot handles most of the HTTP work for you, learning **Servlets** and **JSP** helps you understand how Java web apps work under the hood.

---

## 🧩 What Are Servlets?

A **Servlet** is a Java class that handles HTTP requests and responses. It runs on a Java-enabled web server (like Apache Tomcat).

---

## 📦 Basic Servlet Lifecycle

| Phase      | Method         | Description                        |
|------------|----------------|------------------------------------|
| Initialization | `init()`      | Called once when servlet loads     |
| Request Handling | `doGet()`, `doPost()` | Called per request         |
| Destruction | `destroy()`   | Called when servlet is unloaded    |

---

## ✅ Simple `doGet()` Example

```java
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        res.setContentType("text/html");
        res.getWriter().println("<h1>Hello from Servlet!</h1>");
    }
}
```

### 🔍 How It Works:
-	**@WebServlet("/hello")** maps the class to the /hello URL.
-	**doGet()** handles GET requests.
-	**getWriter()** writes HTML to the browser.

## 💬 doPost() for Form Handling

```java
@WebServlet("/submit")
public class FormServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        String name = req.getParameter("name");
        res.getWriter().println("Welcome, " + name);
    }
}
```
## 🖼️ What is JSP?

JSP (JavaServer Pages) allows you to mix HTML and Java code to generate dynamic web pages.
```java
<!-- hello.jsp -->
<html>
<body>
    <h2>Welcome <%= request.getParameter("name") %></h2>
</body>
</html>
```

## 🔄 When Should You Learn Servlets & JSP?
```text
| Use Case                  | Recommendation                          |
|---------------------------|-----------------------------------------|
| Learning how HTTP works   | ✅ Good to understand the basics        |
| Real project development  | ❌ Use Spring Boot instead              |
```

##  Summary
```text
| Concept      | Purpose                                       |
|--------------|-----------------------------------------------|
| Servlet      | Java class that handles web requests          |
| `@WebServlet`| Maps servlet to a specific URL                |
| `doGet()`    | Handles GET requests                          |
| `doPost()`   | Handles POST requests                         |
| JSP          | Mixes Java with HTML (now considered legacy)  |
```
