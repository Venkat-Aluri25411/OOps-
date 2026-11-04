# Day 09: Method Overloading in Java – Part 1

## 1. What Is Method Overloading?

When two or more methods have the same name but different parameter lists, they are said to be overloaded methods.

Methods can differ by:
- Number of arguments.
- Type of arguments.
- Order of argument types.

### Example

```java
class Test {

    void m1() {
        System.out.println("No arguments");
    }

    void m1(int a) {
        System.out.println("Integer argument");
    }

    void m1(double a) {
        System.out.println("Double argument");
    }
}
```

Here, three methods have the same name `m1()`, but their parameter lists are different.

This is called **method overloading**.

---

## 2. Why Do We Need Method Overloading?

In C, functions cannot be overloaded based on their parameter types.

For example, the C standard library provides different function names for different operations:

```c
abs(int value);
labs(long value);
llabs(long long value);
```

We use different function names for different argument types.

In Java, we can use the same method name with different parameter lists.

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    long add(long a, long b) {
        return a + b;
    }
}
```

### Advantages of Method Overloading

1. **Code readability:** We can use the same method name for logically similar operations.
2. **Flexibility:** The same operation can work with different types and numbers of arguments.
3. **Reduced naming complexity:** We do not need separate method names for every variation of an operation.

---

## 3. Method Resolution in Overloading

Method resolution means identifying which overloaded method should execute when a method is called.

In Java, method overloading is resolved by the compiler during compilation.

It is also known as:

- Compile-time polymorphism
- Static polymorphism
- Early binding

### Example

```java
class Test {

    void m1(int a) {
        System.out.println("Integer method");
    }

    void m1(double a) {
        System.out.println("Double method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1(10);
        t.m1(10.5);
    }
}
```

Output:

```text
Integer method
Double method
```

The compiler selects the appropriate overloaded method based on the argument types and applicable conversion rules.

**Important:** Overloading resolution is not based simply on the reference type of the object. It is primarily based on the compile-time types of the arguments and the available method declarations.

---

## 4. Automatic Promotion in Method Overloading

What happens when an exact matching method is not available?

Java tries to promote the argument to another compatible type using primitive widening conversions.

This is called **automatic promotion**.

### Example 1: Character to Integer

```java
class Test {

    void m1(int i) {
        System.out.println("Integer method");
    }

    void m1(float f) {
        System.out.println("Float method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        t.m1('a');
    }
}
```

Output:

```text
Integer method
```

### Explanation

Here, the argument is:

```java
t.m1('a');
```

The argument type is `char`.

There is no exact matching `m1(char)` method.

Java checks compatible widening conversions:

```text
char → int
```

Therefore, `m1(int)` is selected.

This is called automatic promotion.

---

## 5. Primitive Widening Promotion Order

The commonly used widening paths are:

```text
byte → short → int → long → float → double

char → int → long → float → double
```

Important:
- `char` can be promoted to `int`, but not to `short`.
- `boolean` cannot be converted to another primitive type.
- Widening does not mean every type can be converted to every other type.
- `double` has no wider primitive numeric type.

### Example 2: Byte to Integer

```java
class Test {

    void m1(short s) {
        System.out.println("Short method");
    }

    void m1(int i) {
        System.out.println("Integer method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        byte b = 10;
        t.m1(b);
    }
}
```

Output:

```text
Short method
```

### Explanation

The argument is `byte`.

Possible widening conversions include:

```text
byte → short
byte → int
byte → long
```

Java selects the most specific applicable method, which is `m1(short)`.

### Example 3: Double Argument

```java
class Test {

    void m1(float f) {
        System.out.println("Float method");
    }

    void m1(int i) {
        System.out.println("Integer method");
    }

    public static void main(String[] args) {

        Test t = new Test();

        double d = 10.5;
        t.m1(d);
    }
}
```

**Result:** Compilation error.

Reason:

- `double` cannot be widened to `float`.
- `double` cannot be widened to `int`.
- Java does not automatically perform narrowing conversions for method overloading.

---

## 6. Important Rules to Remember

1. Java first looks for applicable methods with the given name and argument list.
2. An exact match is preferred over a method requiring conversion.
3. If an exact match is unavailable, Java considers applicable widening conversions.
4. If no applicable method is found, a compilation error occurs.
5. If multiple applicable methods are equally specific, the call can be ambiguous and produce a compilation error.

**Interview answer: What is automatic promotion in method overloading?**

"Automatic promotion is the process in which Java automatically converts a smaller compatible primitive type into a wider primitive type when an exact matching overloaded method is not available. For example, if a method accepts an integer and we pass a character, Java can promote the character to an integer and execute the integer method."