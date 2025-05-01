# 🧵 Multithreading in Java

Multithreading allows concurrent execution of two or more parts of a program for maximum CPU utilization.

---

## 🔹 What is a Thread?

A **thread** is a lightweight subprocess, the smallest unit of execution. Java supports multithreading using:

1. The `Thread` class
2. The `Runnable` interface
3. The `ExecutorService` framework

---

## 🔸 Creating Threads in Java

###  1. Extending the Thread Class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}
MyThread t1 = new MyThread();
t1.start(); // Always use start(), not run()
```
### 2. Implementing Runnable Interface


```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running: " + Thread.currentThread().getName());
    }
}
Thread t = new Thread(new MyRunnable());
t.start();
```
- Preferred for real-world use — avoids Java’s single inheritance limitation.

### Thread Lifecycle
```text
| State          | Description                                |
|----------------|--------------------------------------------|
| New            | Thread is created but not started          |
| Runnable       | start() is called, thread is ready         |
| Running        | Thread is actively executing               |
| Blocked/Waiting| Thread is paused (sleep, wait, join)       |
| Terminated     | Thread has finished execution              |
```
### Thread Methods
```text
| Method    | Description                                |
|-----------|--------------------------------------------|
| start()   | Begins execution of the thread             |
| run()     | Entry point (called internally by start()) |
| sleep(ms) | Pauses thread temporarily                  |
| join()    | Waits for another thread to finish         |
| isAlive() | Checks if thread is still running          |
```
```java
Thread.sleep(1000); // Pause for 1 second
t1.join();          // Wait for t1 to finish before moving on
```

### Synchronization

Used to prevent race conditions when multiple threads access shared resources.
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }
}
```
#### ➤ synchronized keyword
-	**On methods**: locks the whole method for one thread at a time.
-	**On blocks**: allows fine-grained locking.
```java
synchronized(this) {
    // critical section
}
```
### Volatile Keyword

Ensures visibility of changes to variables across threads.
```java
volatile boolean isRunning = true;
```
Without volatile, one thread might not see the updated value written by another thread (due to CPU caching).

### Thread Safety

A method or class is thread-safe if it behaves correctly when accessed by multiple threads.

 Not Thread-Safe Example
```java
List<Integer> list = new ArrayList<>();
// Multiple threads adding to list -> may cause ConcurrentModificationException
```
### Thread-Safe Alternatives
```text
| Task             | Thread-Safe Option                                     |
|------------------|--------------------------------------------------------|
| List operations  | Collections.synchronizedList() or CopyOnWriteArrayList |
| Map operations   | ConcurrentHashMap                                      |
| Custom sync      | Use synchronized blocks or methods                     |
```
### ExecutorService (Thread Pool)

A modern, scalable way to manage multiple threads efficiently.
```java
ExecutorService executor = Executors.newFixedThreadPool(2);

executor.submit(() -> {
    System.out.println("Running in executor: " + Thread.currentThread().getName());
});

executor.shutdown(); // Important: Always shut down the executor
```
### Types of Thread Pools
```text

| Type                      | Use Case                             |
|---------------------------|--------------------------------------|
| newFixedThreadPool(n)     | Limited number of threads            |
| newCachedThreadPool()     | Dynamic resizing (for shortks)       |
| newSingleThreadExecutor() | Single background thread             |
```
### Real-world Example: Quiz App Timer
```java
class Countdown extends Thread {
    public void run() {
        for (int i = 5; i >= 1; i--) {
            System.out.println("Timer: " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println("Timer interrupted");
            }
        }
    }
}
```
### Common Issues in Multithreading
```text
| Issue               | Description                                                        |
|---------------------|--------------------------------------------------------------------|
| Race condition      | Two threads updating shared data simultaneously                    |
| Deadlock            | Two threads waiting on each other forever                          |
| Starvation          | Low-priority thread never gets CPU time                            |
| Livelock            | Threads keep reacting to each other and never progress             |
| Memory inconsistency| One thread sees stale value (use `volatile` or synchronization)    |
```

### Best Practices
-	Prefer ExecutorService over manually managing threads.
-	Always handle InterruptedException properly.
-	Use synchronized or thread-safe collections for shared data.
-	Avoid long operations in the main thread (especially in GUI apps).
-	Minimize the synchronized block size (lock only critical code).

### Summary
```text
| Concept        | Usage                            | Example                       |
|----------------|----------------------------------|-------------------------------|
| Thread class   | Create new thread                | extends Thread                |
| Runnable       | Implement task logic             | implements Runnable           |
| ExecutorService| Thread pool management           | Executors.newFixedThreadPool()|
| synchronized   | Locking shared resources         | synchronized void method()    |
| volatile       | Ensure visibility across threads | volatile boolean flag         |
| join()         | Wait for another thread          | t1.join()                     |


```

✅ Next: [File Handling](File-Handling.md)
