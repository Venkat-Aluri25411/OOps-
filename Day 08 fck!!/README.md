# Day 08: Cyclic Inheritance and Method Signature in Java

# 1. Cyclic Inheritance

## What is Cyclic Inheritance?

When a class directly or indirectly inherits from itself, it is called cyclic inheritance.

In simple words, a circular relationship is created between classes.

Java does not support cyclic inheritance because a class cannot be its own superclass, either directly or indirectly.

### Scenario 1: A class extending itself

```java
class A extends A {
}
```

**Result:** Compilation error.

Reason: Class `A` cannot inherit from itself.

### Scenario 2: Two classes extending each other

```java
class A extends B {
}

class B extends A {
}
```

**Inheritance diagram:**

```text
      ┌─────────┐
      │    A    │
      └────┬────┘
           │ extends
           ▼
      ┌─────────┐
      │    B    │
      └────┬────┘
           │ extends
           └──────────► A
```

**Result:** Compilation error due to cyclic inheritance.

Here:
- `A` requires `B` as its parent.
- `B` requires `A` as its parent.
- This creates a circular dependency.

A class hierarchy must form a valid inheritance tree, not a cycle.

### Is cyclic inheritance supported in Python?

No. Python also does not allow a class to inherit from itself or form a circular inheritance hierarchy.

Example:

```python
class A(A):
    pass
```

This fails because `A` is not defined when Python tries to create the class.

**Interview answer:**

"Cyclic inheritance occurs when a class directly or indirectly inherits from itself. Java does not support it because it creates a circular inheritance dependency and an invalid class hierarchy."

---

# 2. Polymorphism

**Definition:** Polymorphism means one name or interface can represent multiple forms of behavior.

In Java, the two commonly discussed types are:

1. Compile-time polymorphism — Method overloading.
2. Runtime polymorphism — Method overriding.

---

# 3. Method Signature in Java

## What is a Method Signature?

A method signature consists of:

1. Method name.
2. Parameter types and their order.

**Syntax:**

```java
methodName(parameterTypes)
```

### Example

```java
void m1(int a, float b) {
}

void m2(String name) {
}
```

Their method signatures are:

```text
m1(int, float)
m2(String)
```

### Important: Is the return type part of the method signature?

No. In Java, the return type is not part of the method signature.

Example:

```java
class Test {

    int m1(int a) {
        return a;
    }

    float m1(int a) {
        return a;
    }
}
```

**Result:** Compilation error.

Why?

Both methods have the same signature:

```text
m1(int)
```

Only their return types are different. Java cannot overload methods based only on their return types.

### Correct example

```java
class Test {

    int m1(int a) {
        return a;
    }

    float m1(float a) {
        return a;
    }
}
```

These methods have different signatures:

```text
m1(int)
m1(float)
```

Therefore, method overloading is valid.

---

# 4. Important Rules of Method Signatures

| Method declarations | Valid or invalid? |
|---|---|
| Same name, different parameter types | Valid |
| Same name, different number of parameters | Valid |
| Same name, different order of parameter types | Valid |
| Same name and same parameter types, different return type | Invalid |
| Different method names, same parameter types | Valid |

Example:

```java
class Test {

    void m1(int a, float b) {
    }

    void m1(float a, int b) {
    }

    void m1(int a) {
    }

    void m2(int a) {
    }
}
```

All these declarations are valid because their method signatures are different.

---

# 5. How Does the Compiler Resolve Method Calls?

Consider this example:

```java
class Test {

    void m1(int a) {
        System.out.println("Integer method");
    }

    void m1(String a) {
        System.out.println("String method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1(10);
        t.m1("Hello");
    }
}
```

Output:

```text
Integer method
String method
```

### Explanation

When the compiler encounters:

```java
t.m1(10);
```

It checks the available methods and finds that `m1(int)` is the appropriate match.

When it encounters:

```java
t.m1("Hello");
```

It finds that `m1(String)` is the appropriate match.

If no applicable method can be found, the compiler reports an error.

EX->

```class Test {
    void display(int a) {
        System.out.println("A");
    }

    void display(float a) {
        System.out.println("B");
    }

    public static void main(String[] args) {
        Test t = new Test();
        t.display(10);
    }
}```

**Important:** The compiler performs overload resolution using the method name, argument types, and applicable conversion rules. It does not simply compare method names.

---

# 6. Important Interview Points

1. Method signature = method name + parameter types.
2. Return type is not part of a Java method signature.
3. Method overloading is an example of compile-time polymorphism.
4. Two methods in the same class cannot have the same signature.
5. Changing only the return type does not create a valid overloaded method.
6. The compiler checks whether a suitable method is available during compilation.

**Correction regarding C++:** C++ also does not allow functions to be overloaded based only on their return types. Java and C++ both use parameter lists to distinguish overloaded functions.