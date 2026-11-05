# Day 10: Method Overloading in Java – Part 2 to Part 6

# Part 2: Method Overloading with Parent and Child Reference Types

Consider a class containing two overloaded methods:

- One method accepts `Object`.
- Another method accepts `String`.

```java
class Test {

    void m1(Object o) {
        System.out.println("Object method");
    }

    void m1(String s) {
        System.out.println("String method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1(new Object());
        t.m1("Venkat");
        t.m1(null);
    }
}
```

### Output

```text
Object method
String method
String method
```

### Explanation

**Case 1:**

```java
t.m1(new Object());
```

The argument is an `Object` instance.

Therefore, the `m1(Object)` method gets executed.

**Case 2:**

```java
t.m1("Venkat");
```

The argument is a `String` instance.

Therefore, the exact matching `m1(String)` method gets executed.

**Case 3:**

```java
t.m1(null);
```

Here, both `Object` and `String` can accept `null` because they are reference types.

But `String` is a child class of `Object`.

Therefore, Java selects the more specific method, `m1(String)`.

**Important rule:**

When multiple overloaded methods are applicable for a `null` argument, Java selects the most specific applicable parameter type.

---

# Part 3: Method Overloading with Unrelated Classes

Consider two overloaded methods:

- One accepts `String`.
- Another accepts `StringBuffer`.

Both are unrelated classes.

```java
class Test {

    void m1(String s) {
        System.out.println("String method");
    }

    void m1(StringBuffer sb) {
        System.out.println("StringBuffer method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1("Venkat");

        t.m1(new StringBuffer("Hello"));

        t.m1(null);
    }
}
```

### Output

The first two calls are valid:

```text
String method
StringBuffer method
```

But the third call:

```java
t.m1(null);
```

Produces a compilation error.

### Why?

Both `String` and `StringBuffer` can accept `null`.

However:

- `String` is not a parent of `StringBuffer`.
- `StringBuffer` is not a parent of `String`.

Neither parameter type is more specific than the other.

Therefore, the compiler cannot decide which method should execute.

This is called an **ambiguous method call** or **ambiguous reference error**.

**Important distinction:**

| Overloaded parameter types | Result for `null` |
|---|---|
| `Object` and `String` | String method |
| `Object` and `StringBuffer` | StringBuffer method |
| `String` and `StringBuffer` | Compilation error |

---

# Part 4: Method Overloading with Varargs

Varargs means variable-length arguments.

It allows a method to accept zero or more arguments of a specified type.

Syntax:

```java
returnType methodName(dataType... variableName)
```

### Example

```java
class Test {

    void m1(int i) {
        System.out.println("General method");
    }

    void m1(int... i) {
        System.out.println("Varargs method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1();
        t.m1(10);
        t.m1(10, 20);
    }
}
```

### Output

```text
Varargs method
General method
Varargs method
```

### Explanation

**Case 1:**

```java
t.m1();
```

The general method requires one integer argument.

Since no argument is passed, it cannot be selected.

The varargs method accepts zero or more arguments.

Therefore, the varargs method executes.

**Case 2:**

```java
t.m1(10);
```

Both methods can accept one integer argument.

However, Java gives priority to the fixed-arity method over the varargs method.

Therefore, the general method executes.

**Case 3:**

```java
t.m1(10, 20);
```

The general method accepts only one argument.

The varargs method can accept multiple arguments.

Therefore, the varargs method executes.

### Important Rule

Varargs methods have lower priority than applicable fixed-arity methods.

Java considers variable-arity invocation only after the applicable fixed-arity method search phases.

Think of varargs as a flexible fallback when no suitable fixed-arity method is applicable.

---

# Part 5: Method Overloading with Different Parameter Orders

Consider two overloaded methods:

```java
class Test {

    void m1(int i, float f) {
        System.out.println("int-float method");
    }

    void m1(float f, int i) {
        System.out.println("float-int method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1(10, 10.5f);

        t.m1(10.5f, 10);

        t.m1(10, 10);

        t.m1(10.5f, 10.5f);
    }
}
```

### Case 1

```java
t.m1(10, 10.5f);
```

Argument types:

```text
int, float
```

Exact matching method:

```java
m1(int i, float f)
```

Output:

```text
int-float method
```

### Case 2

```java
t.m1(10.5f, 10);
```

Argument types:

```text
float, int
```

Exact matching method:

```java
m1(float f, int i)
```

Output:

```text
float-int method
```

### Case 3

```java
t.m1(10, 10);
```

Argument types:

```text
int, int
```

Now Java considers both methods:

**First method:**

```java
m1(int, float)
```

The second argument requires widening:

```text
int → float
```

**Second method:**

```java
m1(float, int)
```

The first argument requires widening:

```text
int → float
```

Both methods are applicable, but neither is more specific than the other.

Therefore, the compiler reports an ambiguous method call.

### Case 4

```java
t.m1(10.5f, 10.5f);
```

Argument types:

```text
float, float
```

First method requires:

```text
float → int
```

Second method also requires:

```text
float → int
```

These are narrowing conversions.

Java does not automatically perform these conversions for method invocation.

Therefore, no applicable method is found, resulting in a compilation error.

### Summary

| Method call | Result |
|---|---|
| `t.m1(10, 10.5f)` | `int-float` method |
| `t.m1(10.5f, 10)` | `float-int` method |
| `t.m1(10, 10)` | Ambiguous call |
| `t.m1(10.5f, 10.5f)` | No applicable method |

---

# Part 6: Method Overloading with Parent and Child Classes

Consider two classes:

- `Animal` — Parent class.
- `Monkey` — Child class.

```java
class Animal {
}

class Monkey extends Animal {
}

class Test {

    void m1(Animal a) {
        System.out.println("Animal method");
    }

    void m1(Monkey m) {
        System.out.println("Monkey method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        Animal a = new Animal();
        Monkey m = new Monkey();

        Animal a1 = new Monkey();

        t.m1(a);
        t.m1(m);
        t.m1(a1);
    }
}
```

### Output

```text
Animal method
Monkey method
Animal method
```

### Explanation

**Case 1:**

```java
Animal a = new Animal();
t.m1(a);
```

The reference type is `Animal`.

Therefore, `m1(Animal)` is selected.

**Case 2:**

```java
Monkey m = new Monkey();
t.m1(m);
```

The reference type is `Monkey`.

The compiler selects the more specific matching method, `m1(Monkey)`.

**Case 3:**

```java
Animal a1 = new Monkey();
t.m1(a1);
```

This is an important case.

Here:

- Reference type = `Animal`.
- Actual object type = `Monkey`.

The compiler resolves the overloaded method using the compile-time reference type.

Therefore, `m1(Animal)` is selected.

Even though the actual object is `Monkey`, the overloaded `m1(Monkey)` method is not selected.

### Important Rule

In method overloading, method resolution is based on the compile-time types of the arguments, not their actual runtime object types.

This is called compile-time polymorphism or static binding.

**Do not confuse this with method overriding:**

- Overloading: Resolved at compile time using argument types.
- Overriding: Runtime method dispatch selects the implementation based on the actual object type.