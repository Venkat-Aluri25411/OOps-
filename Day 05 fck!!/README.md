# Day 06: Inheritance in Java

## 1. Why Do We Need Inheritance?

Consider a system with three loan classes:

- `HomeLoan`
- `CarLoan`
- `PersonalLoan`

Suppose each class contains 300 methods, and 100 of those methods are common to all three classes.

Without inheritance, we may need to duplicate common methods across all three classes. This increases code duplication and makes maintenance harder.

**Solution:** Create a separate parent class containing the common methods, and let the three loan classes inherit those methods.

### Example

```java
class Loan {
    void calculateInterest() {
        System.out.println("Calculating interest");
    }

    void generateStatement() {
        System.out.println("Generating statement");
    }
}

class HomeLoan extends Loan {
    void processHomeLoan() {
        System.out.println("Processing home loan");
    }
}

class CarLoan extends Loan {
    void processCarLoan() {
        System.out.println("Processing car loan");
    }
}

class PersonalLoan extends Loan {
    void processPersonalLoan() {
        System.out.println("Processing personal loan");
    }
}
```

Each child class can use the common methods inherited from `Loan` without rewriting them.

**Advantages of inheritance:**
- Code reusability
- Reduced code duplication
- Easier maintenance
- Reduced development effort

Inheritance is useful when classes have a genuine *IS-A* relationship, not merely because some methods happen to be identical.

---

## 2. Root Classes in Java

### Which class is the root of the Java class hierarchy?

The `Object` class.

Every Java class ultimately inherits from `java.lang.Object`, either directly or through another superclass. If a class does not explicitly extend another class, it implicitly extends `Object`.

```java
class Student {
    // Implicitly extends Object
}
```

This is effectively equivalent to:

```java
class Student extends Object {
}
```

The `Object` class provides methods that are broadly useful for objects, including:

- `toString()`
- `equals(Object obj)`
- `hashCode()`
- `getClass()`
- `clone()` — protected
- `finalize()` — deprecated and not recommended for use

It also declares `wait()`, `notify()`, and `notifyAll()` for thread coordination.

**Important:** `Object` declares 11 methods in the traditional Java API count, including the three overloaded `wait()` methods as separate declarations. Some lists count the methods differently depending on whether they count overloads separately.

### Which class is the root of Java's exception hierarchy?

The `Throwable` class.

The main hierarchy is:

```text
                 Object
                    |
                Throwable
                /       \
             Error     Exception
                         |
                 RuntimeException
```

- `Throwable` is the superclass of `Error` and `Exception`.
- `Error` represents serious problems that applications generally should not try to handle.
- `Exception` represents conditions applications may need to handle.
- `RuntimeException` is a subclass of `Exception` and includes unchecked exceptions such as `NullPointerException`.

**Why does `Throwable` act as the root?**

It defines common exception-related functionality, including retrieving messages, printing stack traces, and maintaining the cause of an exception. Its subclasses inherit this functionality.

**Proof using Java documentation:** The official Java API documents `Object` as the root of the class hierarchy and `Throwable` as the superclass of all errors and exceptions.

- Object: https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html
- Throwable: https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Throwable.html

---

## 3. Types of Inheritance in Java

### 3.1 Single Inheritance

A child class inherits from one parent class.

```text
┌─────────┐
│    A    │
└────┬────┘
     │
     ▼
┌─────────┐
│    B    │
└─────────┘
```

```java
class A {
    void display() {
        System.out.println("Class A");
    }
}

class B extends A {
}
```

Here, `B` inherits from `A`.

### 3.2 Multiple Inheritance

A single child class inherits from more than one parent class.

```text
┌─────────┐       ┌─────────┐
│    A    │       │    B    │
└────┬────┘       └────┬────┘
     │                 │
     └────────┬────────┘
              ▼
         ┌─────────┐
         │    C    │
         └─────────┘
```

**Java does not support multiple inheritance through classes.**

For example, this is invalid:

```java
class A {
}

class B {
}

class C extends A, B {  // Compilation error
}
```

Java supports multiple inheritance of type through interfaces:

```java
interface A {
    void methodA();
}

interface B {
    void methodB();
}

class C implements A, B {
    public void methodA() {
    }

    public void methodB() {
    }
}
```

### 3.3 Multilevel Inheritance

A class inherits from a child class, creating a chain of inheritance.

```text
┌─────────┐
│    A    │
└────┬────┘
     │
     ▼
┌─────────┐
│    B    │
└────┬────┘
     │
     ▼
┌─────────┐
│    C    │
└─────────┘
```

```java
class A {
}

class B extends A {
}

class C extends B {
}
```

Here, `B` inherits from `A`, and `C` inherits from `B`. Therefore, `C` can inherit accessible members from both `B` and `A`.

### 3.4 Hierarchical Inheritance

Multiple child classes inherit from the same parent class.

```text
             ┌─────────┐
             │    A    │
             └────┬────┘
                  │
          ┌───────┴───────┐
          ▼               ▼
     ┌─────────┐     ┌─────────┐
     │    B    │     │    C    │
     └─────────┘     └─────────┘
```

```java
class A {
    void display() {
        System.out.println("Common method");
    }
}

class B extends A {
}

class C extends A {
}
```

Both `B` and `C` inherit from `A`.

### 3.5 Hybrid Inheritance

Hybrid inheritance combines two or more types of inheritance.

For example, it may combine hierarchical and multiple inheritance.

Java **does not support hybrid inheritance through classes when it requires multiple inheritance**, but hybrid structures can be implemented using interfaces.

---

## 4. Quick Revision

| Type | Meaning | Supported in Java classes? |
|---|---|---|
| Single | One parent, one child | Yes |
| Multiple | One child, multiple parents | No |
| Multilevel | A chain of inheritance | Yes |
| Hierarchical | One parent, multiple children | Yes |
| Hybrid | Combination of inheritance types | Not fully through classes; interfaces can support it |

### Interview answer: Why is inheritance useful?

"Inheritance is an OOP feature that allows a child class to acquire accessible fields and methods from a parent class. It promotes code reusability and reduces duplication. In Java, we use the `extends` keyword for class inheritance and `implements` for implementing interfaces."