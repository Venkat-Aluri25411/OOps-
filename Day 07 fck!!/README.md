# Day 07: Why Java Does Not Support Multiple Inheritance Through Classes

## 1. What Is Multiple Inheritance?

Multiple inheritance means a child class inherits from more than one parent class.

Suppose we have two parent classes, `P1` and `P2`, and one child class, `C`.

- `P1` contains a method named `m1()`.
- `P2` also contains a method named `m1()`.
- `C` inherits from both parents.

If we create an object of `C` and call `c.m1()`, which parent's implementation should execute?

Should it execute `P1.m1()` or `P2.m1()`?

This can create **ambiguity**, also called the *diamond problem* in a common multiple-inheritance scenario.

Java avoids this ambiguity by not allowing a class to extend more than one class.

```java
class P1 {
    void m1() {
        System.out.println("P1 method");
    }
}

class P2 {
    void m1() {
        System.out.println("P2 method");
    }
}

// Invalid Java syntax:
class C extends P1, P2 {
}
```

The code produces a compilation error because Java does not allow a class to extend multiple classes.

**Important:** Ambiguity is one reason for this design, but it is not the only possible concern with multiple inheritance.

---

## 2. What Is the Diamond Problem?

Consider this inheritance structure:

```text
        A
       / \
      B   C
       \ /
        D
```

Suppose `A` defines `m1()`, and both `B` and `C` override `m1()`.

When `D` inherits from both `B` and `C`, which implementation should it use?

```text
       A: m1()
       /      \
 B: m1()    C: m1()
       \      /
        D
```

There are two possible implementations available through the inheritance paths. This creates a conflict unless the language defines a resolution rule.

Java avoids this particular class-inheritance conflict by disallowing multiple inheritance of classes.

---

## 3. How Does Java Support Multiple Inheritance Through Interfaces?

An interface can declare methods without providing their implementations. A class can implement multiple interfaces.

Suppose we have two interfaces, `PI1` and `PI2`, and a child interface `CI`.

Both parent interfaces declare `m1()`, but neither provides a method body.

```java
interface PI1 {
    void m1();
}

interface PI2 {
    void m1();
}

interface CI extends PI1, PI2 {
}
```

This is valid Java.

Why? Both declarations have the same method signature and are abstract interface methods. There are no competing method implementations to choose between.

A class implementing `CI` can provide one implementation that satisfies both inherited declarations.

```java
class C implements CI {
    public void m1() {
        System.out.println("C method");
    }
}

class Main {
    public static void main(String[] args) {
        C c = new C();
        c.m1();
    }
}
```

Output:

```text
C method
```

**Correction:** The child interface `CI` does not itself execute the method. The concrete class `C` provides the implementation, and the object executes it when `m1()` is called.

Also, an interface can extend multiple interfaces, while a class can implement multiple interfaces.

---

## 4. What If Both Interfaces Have Default Methods?

Default methods contain implementations, so conflicts can occur.

```java
interface PI1 {
    default void m1() {
        System.out.println("PI1 method");
    }
}

interface PI2 {
    default void m1() {
        System.out.println("PI2 method");
    }
}

class C implements PI1, PI2 {
    @Override
    public void m1() {
        PI1.super.m1();
        // Or use your own implementation.
    }
}
```

Here, `C` must resolve the conflict by overriding `m1()`. Inside the override, it can explicitly call `PI1.super.m1()` or `PI2.super.m1()`, or provide completely different behavior.

**Important:** Multiple inheritance through interfaces is supported, but Java does not automatically choose one of two conflicting default implementations.

---

## 5. Does Python Support Multiple Inheritance?

Yes. Python supports multiple inheritance through classes.

```python
class P1:
    def m1(self):
        print("P1 method")

class P2:
    def m1(self):
        print("P2 method")

class C(P1, P2):
    pass

c = C()
c.m1()
```

Output:

```text
P1 method
```

Python uses the **Method Resolution Order (MRO)** to decide which method to find first. In this example, `P1` appears before `P2` in `C`'s parent list, so Python searches `P1` first.

You can inspect the order with:

```python
print(C.mro())
```

Python's behavior is not simply an arbitrary choice: it follows a defined algorithm called C3 linearization.

---

## 6. Direct and Indirect Subclasses of `Object`

Every Java class ultimately inherits from `Object`.

### Case 1: A class does not explicitly extend another class

```java
class Student {
}
```

This class implicitly extends `Object`.

```text
Object
   |
Student
```

`Student` is a **direct subclass** of `Object`.

### Case 2: A class extends another class

```java
class Person {
}

class Student extends Person {
}
```

The hierarchy becomes:

```text
Object
   |
 Person
   |
 Student
```

Here:

- `Person` is a direct subclass of `Object`.
- `Student` is an indirect subclass of `Object`.
- `Student` inherits accessible members from its superclass chain.

Even if a class explicitly extends a parent class, it ultimately inherits from `Object` through that chain.