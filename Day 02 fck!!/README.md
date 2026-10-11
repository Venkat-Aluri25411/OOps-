# Day 2 — Abstract Classes and Abstract Methods in Java

## 1. Abstract Modifier

The `abstract` modifier is used with **classes and methods**, but not with variables.

- **Abstract class:** A class declared using the `abstract` keyword.
- **Abstract method:** A method declared without an implementation (method body).

### Syntax

```java
abstract class Vehicle {
    abstract int getNumberOfWheels();
}
```

## 2. What Is an Abstract Method?

An abstract method has only a declaration and does not contain a method body.

It ends with a semicolon (`;`) instead of curly braces.

**Syntax:**

```java
public abstract void m1();
```

### Real-Time Example 1: Vehicle

Different vehicles have different numbers of wheels.

- A bike has 2 wheels.
- A car has 4 wheels.
- A truck commonly has 6 or more wheels.

If we define a general `Vehicle` class, we may not want to specify the number of wheels until we know the particular vehicle.

Therefore, we can declare an abstract method in `Vehicle` and let specific vehicle classes implement it.

```java
abstract class Vehicle {
    abstract int getNumberOfWheels();
}

class Bike extends Vehicle {
    @Override
    int getNumberOfWheels() {
        return 2;
    }
}

class Car extends Vehicle {
    @Override
    int getNumberOfWheels() {
        return 4;
    }
}
```

**Explanation:**

- `Vehicle` declares what operation is required.
- `Bike` and `Car` provide their own implementations.
- The abstract method does not specify the actual number of wheels.

### Real-Time Example 2: Fruit

Different fruits have different tastes.

For example, an apple may be sweet or sour, while a lemon is typically sour.

We can declare an abstract method in the general `Fruit` class and implement it in specific fruit classes.

```java
abstract class Fruit {
    abstract String getTaste();
}

class Apple extends Fruit {
    @Override
    String getTaste() {
        return "Sweet or sour";
    }
}

class Lemon extends Fruit {
    @Override
    String getTaste() {
        return "Sour";
    }
}
```

**Key point:** An abstract method defines what a subclass must implement, without defining how that operation is performed.

---

## 3. What Is an Abstract Class?

An abstract class is a class declared using the `abstract` keyword.

```java
abstract class Animal {
    abstract void sound();

    void sleep() {
        System.out.println("Animal is sleeping");
    }
}
```

Here:

- `Animal` is an abstract class.
- `sound()` is an abstract method.
- `sleep()` is a concrete method because it has a method body.

An abstract class can contain both abstract and concrete methods.

### Can We Create an Object of an Abstract Class?

**No. We cannot instantiate an abstract class directly.**

```java
abstract class Animal {
    abstract void sound();
}

// Animal a = new Animal(); // Compilation error
```

**Why?**

An abstract class cannot be instantiated directly because it may contain abstract methods that have no implementation.

However, this does not mean that every method in an abstract class lacks an implementation.

### Can an Abstract Class Have Zero Abstract Methods?

**Yes.** An abstract class can contain zero abstract methods.

```java
abstract class Example {
    void display() {
        System.out.println("Hello");
    }
}
```

This is valid Java.

An abstract class can be declared abstract even when all its methods have implementations. For example, some framework classes are abstract to prevent direct instantiation or to provide a base class for subclasses.

---

## 4. Child Class Responsibilities

When a concrete child class extends an abstract class, it must implement all inherited abstract methods that remain unimplemented.

### Case 1: Implement All Abstract Methods

```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

This is valid because `Dog` implements the abstract method `sound()`.

### Case 2: Child Class Does Not Implement All Abstract Methods

```java
abstract class Animal {
    abstract void sound();
    abstract void eat();
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

This produces a compilation error because `Dog` has not implemented `eat()` and is not declared abstract.

### Solution: Declare the Child Class Abstract

```java
abstract class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
```

Now the declaration is valid, even though `Dog` does not implement `eat()`.

**Remember these two rules:**

1. A concrete child class must implement all inherited abstract methods that remain unimplemented.
2. If it does not, the child class must itself be declared abstract.

---

## 5. Can We Call Methods of an Abstract Class?

We cannot create an object of an abstract class directly. However, we can use a concrete subclass object to call inherited concrete methods and implemented abstract methods.

```java
abstract class Animal {
    abstract void sound();

    void sleep() {
        System.out.println("Animal is sleeping");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Main {
    public static void main(String[] args) {
        Dog d = new Dog();

        d.sound();
        d.sleep();
    }
}
```

**Output:**

```text
Dog barks
Animal is sleeping
```

Here, `Dog` provides the implementation of `sound()`, while it inherits the concrete implementation of `sleep()` from `Animal`.

We can also write:

```java
Animal a = new Dog();
a.sound();
a.sleep();
```

This works because the reference type is `Animal`, but the actual object is `Dog`.

---

## 6. What Is an Adapter Class?

An adapter class provides empty implementations of interface methods so that a subclass does not have to implement every method when it needs only a few of them.

This pattern is useful when an interface declares many methods but a class needs to override only some.

### Example: WindowAdapter

Java's AWT library provides the `WindowAdapter` class, which allows us to override only the window events we need.

```java
import java.awt.event.*;

class MyWindow extends WindowAdapter {
    @Override
    public void windowClosing(WindowEvent e) {
        System.out.println("Window is closing");
    }
}
```

Here, `MyWindow` overrides only `windowClosing()` rather than implementing every method declared by `WindowListener`.

**Important distinction:** `WindowAdapter` is an abstract adapter class, not an interface. An adapter class is a convenience implementation of an interface or listener contract, often with empty method bodies.

---

## 7. Quick Interview Revision

| Question | Answer |
|---|---|
| Where is `abstract` applicable? | Classes and methods, not variables |
| What is an abstract method? | A method declared without a body |
| How does an abstract method end? | With a semicolon |
| Can an abstract class contain concrete methods? | Yes |
| Can an abstract class contain zero abstract methods? | Yes |
| Can we instantiate an abstract class directly? | No |
| Must a concrete child implement inherited abstract methods? | Yes, if any remain unimplemented |
| Can an abstract child leave abstract methods unimplemented? | Yes |
| Can a subclass call a concrete method inherited from an abstract class? | Yes |
| What is an adapter class? | A convenience class providing implementations, often empty, for interface methods |

## Final Concept to Remember

**An abstract class provides a common base, and abstract methods define operations that concrete subclasses must implement.**

Abstract classes help us define a common structure while allowing subclasses to provide their own specific behavior.
