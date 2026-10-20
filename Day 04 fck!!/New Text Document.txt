# Day 5 — Encapsulation, Tight Encapsulation, and Inheritance in Java

## 1. Data Hiding

### Definition

**Data hiding is the process of restricting direct access to an object's internal data from outside the class.**

In Java, we commonly achieve data hiding by declaring data members as `private` and providing controlled access through methods.

### Real-Time Examples

**Email account:** A username and password should not be freely modified by external code. Access should be controlled through appropriate methods and validation.

**Bank account:** The account balance should not be directly modified by outside code. Deposits and withdrawals should be validated.

### Java Example

```java
class BankAccount {
    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Here, `balance` is private, so code outside the class cannot access it directly.

### Advantages of Data Hiding

- **Security:** Restricts direct access to internal data.
- **Data integrity:** Prevents uncontrolled modifications.
- **Controlled access:** Validation can be performed before changing data.
- **Maintainability:** Internal data representation can change without necessarily changing the public API.

**Interview answer:** Data hiding restricts direct access to internal data. In Java, it is commonly achieved using private data members and controlled access methods.

---

## 2. Abstraction

### Definition

**Abstraction means exposing essential functionality while hiding unnecessary implementation details.**

It tells the user what a component does without requiring the user to know how it works internally.

### Real-Time Example: ATM

When we use an ATM, we can withdraw money, check the balance, or deposit money without understanding the internal banking system and transaction-processing implementation.

### Java Example

```java
abstract class Payment {
    abstract void pay(double amount);
}

class UpiPayment extends Payment {
    @Override
    void pay(double amount) {
        System.out.println("Payment through UPI: " + amount);
    }
}
```

The abstract class defines the operation, while `UpiPayment` provides its implementation.

### Advantages of Abstraction

- **Reduced complexity:** Users interact with essential functionality.
- **Maintainability:** Implementation can change while the public contract remains stable.
- **Extensibility:** New implementations can be introduced.
- **Modularity:** Components can be organized around clear contracts.

**Interview answer:** Abstraction hides implementation details and exposes essential functionality. In Java, it is achieved through abstract classes and interfaces.

---

## 3. Encapsulation

### Definition

**Encapsulation is the process of bundling data and the methods that operate on that data into a single unit, such as a class.**

### Example

```java
class Student {
    private int age;

    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }

    public int getAge() {
        return age;
    }
}
```

Here:

- `age` stores the data.
- `setAge()` validates and updates the data.
- `getAge()` provides read access.
- All these members belong to the same class.

This is an example of encapsulation, and the private field also demonstrates data hiding.

### Advantages of Encapsulation

1. Controlled access to data.
2. Better data integrity.
3. Improved modularity.
4. Easier maintenance.
5. Flexibility to change internal implementation.

### Does Encapsulation Increase Code Length or Reduce Performance?

Encapsulation may require additional methods, which can increase the amount of code. However, it does not inherently make a Java program slower. Actual performance depends on the implementation and runtime optimizations.

**Important:** Validation has a cost, but that does not mean every method needs complex validation. Validate data where correctness requires it.

### Relationship Between the Concepts

- **Data hiding:** Restricts direct access to internal data.
- **Abstraction:** Hides implementation details and exposes essential functionality.
- **Encapsulation:** Bundles data and related behavior into one unit.

The expression `Encapsulation = Data Hiding + Abstraction` is sometimes used as a simplified interview mnemonic, but it is not a strict definition.

---

## 4. Tightly Encapsulated Class

### Definition

A class is commonly described as **tightly encapsulated** when all its instance variables are declared `private` and access to them is controlled through appropriate methods.

### Example

```java
class Employee {
    private int employeeId;
    private String name;

    public int getEmployeeId() {
        return employeeId;
    }

    public void setEmployeeId(int employeeId) {
        if (employeeId > 0) {
            this.employeeId = employeeId;
        }
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        if (name != null && !name.isBlank()) {
            this.name = name;
        }
    }
}
```

Both instance variables are private, and the class provides controlled access to them.

### Important Interview Point

Under the common textbook definition, if a parent class is not tightly encapsulated, a child class is not considered tightly encapsulated.

This is because a child class may inherit accessible non-private instance variables from its parent, exposing data that is not hidden.

**Remember:** The precise definition of tight encapsulation can vary by textbook. For interviews, explain the rule your syllabus uses and distinguish it from the broader concept of encapsulation.

---

## 5. Inheritance in Java

### Definition

**Inheritance is an OOP feature in which a class acquires accessible members and behavior from another class.**

Inheritance represents an **IS-A relationship**.

### Advantages of Inheritance

- Code reusability.
- Reduced duplication.
- Easier extension of existing classes.
- Support for runtime polymorphism through method overriding.

Java uses the `extends` keyword for class inheritance.

### Example

```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}
```

Here, `Dog` extends `Animal`, so a `Dog` object can use the inherited `eat()` method and its own `bark()` method.

---

## 6. Parent Reference and Child Object

This is one of the most important Java interview concepts.

### Case 1: Parent Reference with Parent Object

```java
Animal a = new Animal();
a.eat();
```

This is valid because the reference type and object type are both `Animal`.

### Case 2: Child Reference with Child Object

```java
Dog d = new Dog();

d.eat();
d.bark();
```

This is valid because `Dog` inherits `eat()` and declares `bark()`.

### Case 3: Parent Reference with Child Object

```java
Animal a = new Dog();

a.eat();
// a.bark(); // Compilation error
```

This is valid.

The reference type is `Animal`, while the actual object is `Dog`.

- `a.eat()` compiles because `eat()` is declared in `Animal`.
- `a.bark()` does not compile because `bark()` is not declared in `Animal`.

**Important rule:** The reference type determines which members can be accessed at compile time. The actual object type determines which overridden instance method implementation runs at runtime.

### Case 4: Child Reference with Parent Object

```java
Dog d = new Animal(); // Compilation error
```

This is invalid because a general `Animal` object is not necessarily a `Dog`.

A child reference cannot directly hold a parent object unless an appropriate, valid conversion is possible. In this example, no such conversion exists.

---

## 7. Inheritance Example with Output

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }

    void eat() {
        System.out.println("Dog eats");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog();

        a.sound();

        // a.eat(); // Compilation error
    }
}
```

**Output:**

```text
Dog barks
```

Although `a` is an `Animal` reference, the actual object is a `Dog`. Therefore, the overridden `sound()` implementation in `Dog` executes.

However, `a.eat()` is a compilation error because `eat()` is not declared in `Animal`.

---

## 8. Quick Interview Revision

| Concept | Key point |
|---|---|
| Data hiding | Restricts direct access to internal data |
| Abstraction | Hides implementation details |
| Encapsulation | Bundles data and related methods |
| Tight encapsulation | Commonly requires all instance variables to be private |
| Inheritance | Represents an IS-A relationship |
| `extends` | Used for class inheritance |
| Parent reference + child object | Can access members declared in the parent type |
| Child reference + child object | Can access inherited accessible members and child-specific members |
| Child reference + parent object | Invalid in ordinary assignment |
| Runtime polymorphism | Overridden method implementation depends on the actual object |

## 9. Final Rules to Remember

1. Private variables cannot be accessed directly from outside their enclosing class.
2. Encapsulation bundles data and related behavior together.
3. Inheritance promotes code reuse and supports polymorphism.
4. The reference type determines compile-time member accessibility.
5. The actual object type determines which overridden instance method implementation runs.
6. A parent reference can hold a child object, but it cannot directly access child-specific methods absent from the parent type.

**Practice task:** Write the four inheritance reference/object combinations and predict which method calls compile before running the program.
