+++
date = '2024-01-01T12:44:47+10:00'
draft = false
title = '🏢 JEE Design Patterns'
tags = ['JEE Design Patterns', 'Interview']
+++

JEE design patterns are specialized solutions for enterprise Java applications. They address scalability, maintainability, and performance challenges in distributed systems, helping developers build robust, modular, and efficient enterprise-grade software.

## Table of Contents

- [Presentation Tier Patterns](#presentation-tier-patterns)
  - [Intercepting Filter](#intercepting-filter)
  - [Front Controller](#front-controller)
  - [View Helper](#view-helper)
  - [Composite View](#composite-view)
- [Business Tier Patterns](#business-tier-patterns)
  - [Business Delegate](#business-delegate)
  - [Session Facade](#session-facade)
  - [Application Service](#application-service)
  - [Service Locator](#service-locator)
  - [Transfer Object](#transfer-object)
- [Integration Tier Patterns](#integration-tier-patterns)
  - [Data Access Object (DAO)](#data-access-object-dao)
  - [Service Activator](#service-activator)
  - [Web Service Broker](#web-service-broker)
- [Summary](#summary)

---

## Presentation Tier Patterns

### Intercepting Filter

Provides centralized request pre-processing and post-processing.

**Example (Java):**
```java
public interface Filter {
    void execute(String request);
}

public class AuthenticationFilter implements Filter {
    public void execute(String request) {
        System.out.println("Authenticating request: " + request);
    }
}

public class FilterChain {
    private List<Filter> filters = new ArrayList<>();
    public void addFilter(Filter filter) { filters.add(filter); }
    public void execute(String request) {
        for (Filter filter : filters) { filter.execute(request); }
    }
}
```

**When to use:**  
- When you need reusable request processing logic (logging, authentication).

**When not to use:**  
- When processing logic is simple or not reusable.

---

### Front Controller

Centralizes request handling to improve control and flexibility.

**Example (Java):**
```java
public class FrontController {
    public void dispatchRequest(String request) {
        if ("HOME".equals(request)) {
            System.out.println("Displaying Home Page");
        } else {
            System.out.println("404 Not Found");
        }
    }
}
```

**When to use:**  
- When you want a single entry point for requests.

**When not to use:**  
- For very simple applications.

---

### View Helper

Separates business logic from view rendering.

**Example (Java):**
```java
public class ViewHelper {
    public String formatDate(Date date) {
        return new SimpleDateFormat("yyyy-MM-dd").format(date);
    }
}
```

**When to use:**  
- When you want to keep views clean and reusable.

**When not to use:**  
- When formatting logic is trivial.

---

### Composite View

Creates views from modular, reusable subviews.

**Example (Java):**
```java
public interface View {
    void render();
}

public class HeaderView implements View {
    public void render() { System.out.println("Header"); }
}

public class CompositeView implements View {
    private List<View> views = new ArrayList<>();
    public void addView(View view) { views.add(view); }
    public void render() {
        for (View view : views) { view.render(); }
    }
}
```

**When to use:**  
- For complex UIs with reusable components.

**When not to use:**  
- For simple, static views.

---

## Business Tier Patterns

### Business Delegate

Decouples presentation and business logic.

**Example (Java):**
```java
public class BusinessService {
    public void doTask() { System.out.println("Business logic executed"); }
}

public class BusinessDelegate {
    private BusinessService service = new BusinessService();
    public void executeTask() { service.doTask(); }
}
```

**When to use:**  
- When you want to hide business logic complexity from the presentation tier.

**When not to use:**  
- When business logic is simple.

---

### Session Facade

Provides a unified interface to a set of business services.

**Example (Java):**
```java
public class OrderService { public void placeOrder() {} }
public class PaymentService { public void processPayment() {} }

public class SessionFacade {
    private OrderService orderService = new OrderService();
    private PaymentService paymentService = new PaymentService();
    public void completeOrder() {
        orderService.placeOrder();
        paymentService.processPayment();
    }
}
```

**When to use:**  
- When you want to reduce network calls and simplify client interaction.

**When not to use:**  
- When only one service is involved.

---

### Application Service

Coordinates business logic across multiple operations.

**Example (Java):**
```java
public class ApplicationService {
    public void performBusinessOperation() {
        // Business logic spanning multiple domain objects
    }
}
```

**When to use:**  
- For complex business workflows.

**When not to use:**  
- For simple, single-step operations.

---

### Service Locator

Centralizes service lookup and management.

**Example (Java):**
```java
public class ServiceLocator {
    private static Map<String, Object> services = new HashMap<>();
    public static Object getService(String name) { return services.get(name); }
    public static void registerService(String name, Object service) { services.put(name, service); }
}
```

**When to use:**  
- When you need to decouple service consumers from service creation.

**When not to use:**  
- When dependency injection is preferred.

---

### Transfer Object

Encapsulates data for transfer between layers.

**Example (Java):**
```java
public class CustomerDTO {
    private String name;
    private String email;
    // getters and setters
}
```

**When to use:**  
- When transferring multiple data fields between layers.

**When not to use:**  
- For simple, single-field transfers.

---

## Integration Tier Patterns

### Data Access Object (DAO)

Abstracts and encapsulates all access to the data source.

**Example (Java):**
```java
public class CustomerDAO {
    public CustomerDTO findCustomerById(int id) {
        // DB lookup logic
        return new CustomerDTO();
    }
}
```

**When to use:**  
- When you want to separate persistence logic from business logic.

**When not to use:**  
- For trivial data access.

---

### Service Activator

Enables asynchronous invocation of business services.

**Example (Java):**
```java
public class ServiceActivator {
    public void activateService(Runnable serviceTask) {
        new Thread(serviceTask).start();
    }
}
```

**When to use:**  
- For asynchronous processing.

**When not to use:**  
- For synchronous, simple calls.

---

### Web Service Broker

Centralizes and manages web service interactions.

**Example (Java):**
```java
public class WebServiceBroker {
    public void callService(String endpoint) {
        System.out.println("Calling web service at " + endpoint);
    }
}
```

**When to use:**  
- For integrating multiple web services.

**When not to use:**  
- For direct, simple web service calls.

---

## Summary

JEE design patterns help solve common problems in enterprise Java applications.  
They improve scalability, maintainability, and modularity, and are essential knowledge for interviews and building robust distributed systems.
