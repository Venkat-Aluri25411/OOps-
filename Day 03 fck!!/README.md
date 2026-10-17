# Java Access Modifiers and Interface Rules

Notes on `public`, `default`, `protected`, and interface implementation in Java, with working and compile-error examples.

---

## 1. Public member access

- A `public` member can be accessed from anywhere, inside the class or outside it.
- But the class itself must also be `public` for outside (other package) access.
- If the class is not public, even a `public` method can't be accessed from outside the package. It gives a compile error.
- Class public + method public → accessible everywhere.
- Class not public (default) → error from other packages, even if the method is public.

### Program 1: Successful (class public + method public)

```java
// File: pack1/A.java
package pack1;

public class A {
    public void show() {
        System.out.println("Hello");
    }
}
```

```java
// File: pack2/B.java
package pack2;
import pack1.A;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.show();
    }
}
```

Output: `Hello`

### Program 2: Compile error (class not public, method public)

```java
// File: pack1/A.java
package pack1;

class A {                    // not public
    public void show() {
        System.out.println("Hello");
    }
}
```

```java
// File: pack2/B.java
package pack2;
import pack1.A;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.show();
    }
}
```

Error: `A is not public in pack1; cannot be accessed from outside package`

The only difference between the two programs is the word `public` before `class A`.

---

## 2. Default access (package-level access)

- If no access modifier is written, the member has default access.
- It can be accessed only within the same package.
- It cannot be accessed from a different package.
- This applies to methods, variables, and classes.

### Example: Works (same package)

```java
// File: pack1/A.java
package pack1;

public class A {
    int x = 10;              // default variable
    void show() {            // default method
        System.out.println("Hello");
    }
}
```

```java
// File: pack1/B.java
package pack1;               // same package

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.show();
        System.out.println(a.x);
    }
}
```

Output:

```
Hello
10
```

### Example: Compile error (different package)

```java
// File: pack2/C.java
package pack2;
import pack1.A;

public class C {
    public static void main(String[] args) {
        A a = new A();
        a.show();            // error
        System.out.println(a.x);   // error
    }
}
```

Error: `show() is not public in A; cannot be accessed from outside package`

Same for `x`: `x is not public in A; cannot be accessed from outside package`

---

## 3. Protected access

- `protected` = default + child classes
- Within the same package: accessible everywhere, no restrictions.
- Outside the package: accessible only in child classes, and only through a **child reference**. A parent reference cannot be used (important).

### Example 1: Same package (works)

```java
// File: pack1/A.java
package pack1;

public class A {
    protected int x = 10;
    protected void show() {
        System.out.println("Hello");
    }
}
```

```java
// File: pack1/B.java
package pack1;

public class B {
    public static void main(String[] args) {
        A a = new A();
        a.show();                    // works
        System.out.println(a.x);     // works
    }
}
```

Output:

```
Hello
10
```

### Example 2: Different package, child reference (works)

```java
// File: pack2/C.java
package pack2;
import pack1.A;

public class C extends A {
    public static void main(String[] args) {
        C c = new C();               // child reference
        c.show();                    // works
        System.out.println(c.x);     // works
    }
}
```

Output:

```
Hello
10
```

### Example 3: Different package, parent reference (compile error)

```java
// File: pack2/D.java
package pack2;
import pack1.A;

public class D extends A {
    public static void main(String[] args) {
        A a = new A();               // parent reference
        a.show();                    // error
        System.out.println(a.x);     // error
    }
}
```

Error: `show() has protected access in pack1.A`

Same for `x`: `x has protected access in pack1.A`

The same applies even if you write `A a = new D();`. The reference type is still `A` (parent), so it is an error.

---

## 4. Interface implementation rules

1. Every method in an interface is `public abstract` by default.
2. When implementing it, the method must be declared `public` (very important). Otherwise it's a compile error, because you can't reduce the visibility when overriding.
3. The class must implement every abstract method of the interface, or it's a compile error.
4. If you don't want to implement all of them, declare the class as `abstract`, since it's only a partial implementation.

### Example 1: Works (public + all methods implemented)

```java
interface Test {
    void m1();
    void m2();
}

class Demo implements Test {
    public void m1() {
        System.out.println("m1");
    }
    public void m2() {
        System.out.println("m2");
    }
    public static void main(String[] args) {
        Demo d = new Demo();
        d.m1();
        d.m2();
    }
}
```

Output:

```
m1
m2
```

### Example 2: Compile error (method not public)

```java
interface Test {
    void m1();
}

class Demo implements Test {
    void m1() {                  // default access, error
        System.out.println("m1");
    }
}
```

Error: `m1() in Demo cannot implement m1() in Test; attempting to assign weaker access privileges; was public`

### Example 3: Compile error (not all methods implemented)

```java
interface Test {
    void m1();
    void m2();
}

class Demo implements Test {
    public void m1() {
        System.out.println("m1");
    }
    // m2() not implemented
}
```

Error: `Demo is not abstract and does not override abstract method m2() in Test`

### Example 4: Works (partial implementation, so class is abstract)

```java
interface Test {
    void m1();
    void m2();
}

abstract class Demo implements Test {
    public void m1() {
        System.out.println("m1");
    }
    // m2() left unimplemented, allowed because Demo is abstract
}
```

This compiles fine. But a child class of `Demo` must then implement `m2()` (as `public`), or it must also be declared `abstract`.