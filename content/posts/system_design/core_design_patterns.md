+++
date = '2025-05-03T12:44:47+10:00'
draft = false
title = '23 Core Design Patterns'
tags = ['Core Design Patterns', 'Interview']
+++

About Core Design Patterns.

## Table of Contents

- [Creational Patterns](#creational-patterns)
  - [Singleton](#singleton)
  - [Factory Method](#factory-method)
  - [Abstract Factory](#abstract-factory)
  - [Builder](#builder)
  - [Prototype](#prototype)
- [Structural Patterns](#structural-patterns)
  - [Adapter](#adapter)
  - [Bridge](#bridge)
  - [Composite](#composite)
  - [Decorator](#decorator)
  - [Facade](#facade)
  - [Flyweight](#flyweight)
  - [Proxy](#proxy)
- [Behavioral Patterns](#behavioral-patterns)
  - [Chain of Responsibility](#chain-of-responsibility)
  - [Command](#command)
  - [Interpreter](#interpreter)
  - [Iterator](#iterator)
  - [Mediator](#mediator)
  - [Memento](#memento)
  - [Observer](#observer)
  - [State](#state)
  - [Strategy](#strategy)
  - [Template Method](#template-method)
  - [Visitor](#visitor)
- [Summary](#summary)

---

## Creational Patterns

### Singleton

Ensures a class has only one instance and provides a global point of access to it.

**Example (Java):**
```java
public class Singleton {
    private static Singleton uniqueInstance;
    private Singleton() {}
    public static synchronized Singleton getInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```

**When to use:**  

- When you need a single shared resource (e.g., config, logger, cache).

**When not to use:**  

- When you need multiple instances (e.g., for testing, parallelism).
- Can introduce hidden dependencies and global state.

---

### Factory Method

Defines an interface for creating an object, but lets subclasses decide which class to instantiate.

**Example (Java):**
```java
public abstract class Animal {
    public abstract String speak();
}

public class Dog extends Animal {
    public String speak() { return "Woof!"; }
}

public class Cat extends Animal {
    public String speak() { return "Meow!"; }
}

public abstract class AnimalFactory {
    public abstract Animal createAnimal();
}

public class DogFactory extends AnimalFactory {
    public Animal createAnimal() { return new Dog(); }
}

public class CatFactory extends AnimalFactory {
    public Animal createAnimal() { return new Cat(); }
}
```

**When to use:**  

- When a class can't anticipate the type of objects it needs to create.

**When not to use:**  

- When object creation is simple and doesn't need abstraction.

---

### Abstract Factory

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Example (Java):**
```java
public interface Button {
    void paint();
}

public class WinButton implements Button {
    public void paint() { System.out.println("Windows Button"); }
}

public class MacButton implements Button {
    public void paint() { System.out.println("Mac Button"); }
}

public interface GUIFactory {
    Button createButton();
}

public class WinFactory implements GUIFactory {
    public Button createButton() { return new WinButton(); }
}

public class MacFactory implements GUIFactory {
    public Button createButton() { return new MacButton(); }
}
```

**When to use:**  

- When you need to create families of related objects.

**When not to use:**  

- When products don't need to be related.

---

### Builder

Separates the construction of a complex object from its representation.

**Example (Java):**
```java
public class Burger {
    private boolean cheese;
    private boolean lettuce;

    public static class Builder {
        private boolean cheese;
        private boolean lettuce;

        public Builder addCheese() {
            cheese = true;
            return this;
        }
        public Builder addLettuce() {
            lettuce = true;
            return this;
        }
        public Burger build() {
            Burger burger = new Burger();
            burger.cheese = this.cheese;
            burger.lettuce = this.lettuce;
            return burger;
        }
    }
}
```

**When to use:**  

- When constructing complex objects step by step.

**When not to use:**  

- For simple objects with few parameters.

---

### Prototype

Creates new objects by copying an existing object.

**Example (Java):**
```java
public abstract class Prototype implements Cloneable {
    public Prototype clone() {
        try {
            return (Prototype) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}
```

**When to use:**  

- When object creation is costly and similar objects are needed.

**When not to use:**  

- When objects are simple or copying is not needed.

---

## Structural Patterns

### Adapter

Allows incompatible interfaces to work together.

**Example (Java):**
```java
public interface USASocket {
    int voltage();
}

public class EuropeanSocket {
    public int voltage() { return 230; }
}

public class SocketAdapter implements USASocket {
    private EuropeanSocket europeanSocket;
    public SocketAdapter(EuropeanSocket socket) {
        this.europeanSocket = socket;
    }
    public int voltage() {
        return europeanSocket.voltage();
    }
}
```

**When to use:**  

- When integrating with legacy or third-party code.

**When not to use:**  

- When you can refactor code directly.

---

### Bridge

Separates abstraction from implementation.

**Example (Java):**
```java
public interface DrawingAPI {
    void drawCircle(int x, int y, int r);
}

public class DrawingAPI1 implements DrawingAPI {
    public void drawCircle(int x, int y, int r) {
        System.out.println("API1: Circle at " + x + "," + y + " radius " + r);
    }
}

public abstract class Shape {
    protected DrawingAPI api;
    public Shape(DrawingAPI api) { this.api = api; }
    public abstract void draw();
}

public class Circle extends Shape {
    private int x, y, r;
    public Circle(int x, int y, int r, DrawingAPI api) {
        super(api);
        this.x = x; this.y = y; this.r = r;
    }
    public void draw() { api.drawCircle(x, y, r); }
}
```

**When to use:**  

- When abstraction and implementation should vary independently.

**When not to use:**  

- When only one implementation is needed.

---

### Composite

Composes objects into tree structures.

**Example (Java):**
```java
public interface Component {
    void operation();
}

public class Leaf implements Component {
    public void operation() { System.out.println("Leaf"); }
}

import java.util.ArrayList;
import java.util.List;

public class Composite implements Component {
    private List<Component> children = new ArrayList<>();
    public void add(Component component) { children.add(component); }
    public void operation() {
        for (Component child : children) {
            child.operation();
        }
    }
}
```

**When to use:**  

- When you need to treat individual and composite objects uniformly.

**When not to use:**  

- When hierarchy is not needed.

---

### Decorator

Adds new functionality to an object dynamically.

**Example (Java):**
```java
public interface Coffee {
    int cost();
}

public class SimpleCoffee implements Coffee {
    public int cost() { return 5; }
}

public class MilkDecorator implements Coffee {
    private Coffee coffee;
    public MilkDecorator(Coffee coffee) { this.coffee = coffee; }
    public int cost() { return coffee.cost() + 2; }
}
```

**When to use:**  

- When you need to add responsibilities to objects dynamically.

**When not to use:**  

- When subclassing is simpler.

---

### Facade

Provides a simplified interface to a complex subsystem.

**Example (Java):**
```java
public class CPU { public void freeze() {} }
public class Memory { public void load(int pos, String data) {} }

public class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    public ComputerFacade() {
        cpu = new CPU();
        memory = new Memory();
    }
    public void start() {
        cpu.freeze();
        memory.load(0, "data");
    }
}
```

**When to use:**  

- When you want to provide a simple interface to a complex system.

**When not to use:**  

- When subsystem is already simple.

---

### Flyweight

Reduces memory usage by sharing data.

**Example (Java):**
```java
import java.util.HashMap;
import java.util.Map;

public class Flyweight {
    private String shared;
    public Flyweight(String shared) { this.shared = shared; }
}

public class FlyweightFactory {
    private Map<String, Flyweight> flyweights = new HashMap<>();
    public Flyweight getFlyweight(String shared) {
        if (!flyweights.containsKey(shared)) {
            flyweights.put(shared, new Flyweight(shared));
        }
        return flyweights.get(shared);
    }
}
```

**When to use:**  

- When many objects share common data.

**When not to use:**  

- When objects are unique.

---

### Proxy

Provides a surrogate for another object.

**Example (Java):**
```java
public interface Subject {
    void request();
}

public class RealSubject implements Subject {
    public void request() { System.out.println("RealSubject"); }
}

public class Proxy implements Subject {
    private RealSubject real;
    public Proxy(RealSubject real) { this.real = real; }
    public void request() {
        System.out.println("Proxy: Checking access");
        real.request();
    }
}
```

**When to use:**  

- For access control, lazy loading, logging.

**When not to use:**  

- When direct access is acceptable.

---

## Behavioral Patterns

### Chain of Responsibility

Passes a request along a chain of handlers.

**Example (Java):**
```java
public abstract class Handler {
    protected Handler next;
    public void setNext(Handler next) { this.next = next; }
    public void handle(String request) {
        if (next != null) next.handle(request);
    }
}
```

**When to use:**  

- When multiple objects can handle a request.

**When not to use:**  

- When only one handler is needed.

---

### Command

Encapsulates a request as an object.

**Example (Java):**
```java
public interface Command {
    void execute();
}

public class LightOnCommand implements Command {
    public void execute() { System.out.println("Light On"); }
}

import java.util.ArrayList;
import java.util.List;

public class Remote {
    private List<Command> commands = new ArrayList<>();
    public void addCommand(Command cmd) { commands.add(cmd); }
    public void run() {
        for (Command cmd : commands) { cmd.execute(); }
    }
}
```

**When to use:**  

- For undo/redo, queuing, logging.

**When not to use:**  

- When simple method calls suffice.

---

### Interpreter

Defines a grammar and provides an interpreter.

**Example (Java):**
```java
public interface Expression {
    int interpret();
}

public class Number implements Expression {
    private int value;
    public Number(int value) { this.value = value; }
    public int interpret() { return value; }
}
```

**When to use:**  

- For languages, expressions, parsing.

**When not to use:**  

- For simple or infrequent grammar.

---

### Iterator

Provides a way to access elements sequentially.

**Example (Java):**
```java
import java.util.Iterator;
import java.util.List;

public class MyIterator implements Iterator<String> {
    private List<String> collection;
    private int index = 0;
    public MyIterator(List<String> collection) { this.collection = collection; }
    public boolean hasNext() { return index < collection.size(); }
    public String next() { return collection.get(index++); }
}
```

**When to use:**  

- When you need to traverse a collection.

**When not to use:**  

- When direct access is sufficient.

---

### Mediator

Encapsulates how objects interact.

**Example (Java):**
```java
public interface Mediator {
    void notify(Component sender, String event);
}

public class Component {
    private Mediator mediator;
    public Component(Mediator mediator) { this.mediator = mediator; }
    public void doSomething() { mediator.notify(this, "event"); }
}
```

**When to use:**  

- When objects communicate in complex ways.

**When not to use:**  

- When communication is simple.

---

### Memento

Captures and restores an object's state.

**Example (Java):**
```java
public class Memento {
    private String state;
    public Memento(String state) { this.state = state; }
    public String getState() { return state; }
}

public class Originator {
    private String state;
    public void setState(String state) { this.state = state; }
    public Memento save() { return new Memento(state); }
    public void restore(Memento memento) { state = memento.getState(); }
}
```

**When to use:**  

- For undo/redo functionality.

**When not to use:**  

- When state is simple or not needed.

---

### Observer

One-to-many dependency so dependents are notified of changes.

**Example (Java):**
```java
import java.util.ArrayList;
import java.util.List;

public interface Observer {
    void update();
}

public class Subject {
    private List<Observer> observers = new ArrayList<>();
    public void attach(Observer obs) { observers.add(obs); }
    public void notifyObservers() {
        for (Observer obs : observers) { obs.update(); }
    }
}
```

**When to use:**  

- For event handling, UI updates.

**When not to use:**  

- When only one object needs notification.

---

### State

Alters behavior when internal state changes.

**Example (Java):**
```java
public interface State {
    void handle();
}

public class Context {
    private State state;
    public Context(State state) { this.state = state; }
    public void request() { state.handle(); }
}
```

**When to use:**  

- When object behavior depends on state.

**When not to use:**  

- When state changes are rare.

---

### Strategy

Encapsulates interchangeable algorithms.

**Example (Java):**
```java
public interface Strategy {
    int execute(int[] data);
}

public class SortStrategy implements Strategy {
    public int execute(int[] data) {
        java.util.Arrays.sort(data);
        return data[0]; // Just for demonstration
    }
}

public class Context {
    private Strategy strategy;
    public Context(Strategy strategy) { this.strategy = strategy; }
    public int doTask(int[] data) { return strategy.execute(data); }
}
```

**When to use:**  

- When multiple algorithms are needed.

**When not to use:**  

- When only one algorithm is used.

---

### Template Method

Defines the skeleton of an algorithm, deferring steps to subclasses.

**Example (Java):**
```java
public abstract class AbstractClass {
    public final void templateMethod() {
        step1();
        step2();
    }
    protected abstract void step1();
    protected abstract void step2();
}

public class ConcreteClass extends AbstractClass {
    protected void step1() { System.out.println("Step 1"); }
    protected void step2() { System.out.println("Step 2"); }
}
```

**When to use:**  

- When algorithms have invariant steps.

**When not to use:**  

- When steps never change.

---

### Visitor

Represents an operation to be performed on elements of an object structure.

**Example (Java):**
```java
public interface Visitor {
    void visit(Element element);
}

public interface Element {
    void accept(Visitor visitor);
}

public class ConcreteElement implements Element {
    public void accept(Visitor visitor) { visitor.visit(this); }
}
```

**When to use:**  

- When you need to perform operations on object structures.

**When not to use:**  

- When object structure rarely changes.

---

## Summary

The 23 core design patterns (Gang of Four) are essential tools for software engineers.  
They provide proven solutions to common problems in software design, improve code maintainability, and are frequently discussed in interviews.  
Understanding these patterns helps you write flexible, scalable, and robust code.
