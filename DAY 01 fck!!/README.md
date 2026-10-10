# Day 1 — Java Basics and Source File Rules

## 1. Multiple Classes in a Single Java File

A Java source file can contain multiple top-level classes, but **at most one top-level class can be `public`** under the usual Java compiler rules.

### Interview / Viva Answer

A Java file can contain multiple classes, but at most one top-level class can be public. If a public class exists, the file name must exactly match the public class name. If there is no public class, the file can be saved with any valid name. The order of classes in the file does not affect compilation.

### Example 1: Public Class Exists

**File name: `StudentDemo.java`**

```java
class Student {
    String name;

    void display() {
        System.out.println("Student name: " + name);
    }
}

public class StudentDemo {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Ravi";

        s1.display();
    }
}
```

**Explanation:**

- `Student` is a non-public class.
- `StudentDemo` is the only public class.
- Therefore, the file must be named `StudentDemo.java`.
- The classes can be declared in a different order without changing the output.

**Output:**

```text
Student name: Ravi
```

### Example 2: No Public Class

**File name: `MyProgram.java`**

```java
class Student {
    String name;

    void display() {
        System.out.println("Student name: " + name);
    }
}

class StudentMain {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Ravi";

        s1.display();
    }
}
```

**Explanation:**

Neither `Student` nor `StudentMain` is public. Therefore, the file can be named `MyProgram.java`, `Day1.java`, or another valid Java source filename.

### Wrong Example 1: Two Public Classes

```java
public class Student {
}

public class StudentDemo {
}
```

**Why is this wrong?**

A single Java source file cannot declare two public top-level classes under the standard file-based Java compilation rules. Each public top-level class must be placed in its appropriately named source file.

### Wrong Example 2: Public Class and Mismatched Filename

**File name: `Day1.java`**

```java
public class Student {
}
```

**Why is this wrong?**

The public class is named `Student`, but the filename is `Day1.java`.

The correct filename is **`Student.java`**.

---

## 2. Java Packages and Import Statements

### 1. Automatic Import of `java.lang`

Java automatically makes the types in the `java.lang` package available. We do not need to explicitly import classes such as `String`, `System`, or `Math`.

```java
public class Main {
    public static void main(String[] args) {
        String name = "Ravi";
        System.out.println(Math.sqrt(25));
    }
}
```

### 2. Classes in the Same Package

Classes belonging to the same package can generally access one another without an import statement, subject to Java's access-control rules.

### 3. Wildcard Import

```java
import java.util.*;
```

This makes accessible types declared directly in `java.util` available by their simple names. It **does not import subpackages** such as `java.util.concurrent`.

### 4. Multiple Classes in One File

A Java source file can contain multiple top-level classes, but at most one can be public under the usual file-based compilation rules.

### 5. Package Statement Position

A source file can have at most one package declaration. If present, it must appear before import declarations and top-level type declarations, apart from comments and applicable annotations.

```java
package mypackage;

import java.util.Scanner;

class Main {
}
```

### 6. Import Statements Are Optional

We can use a fully qualified class name instead of importing a class.

**Without an import:**

```java
java.util.Scanner sc = new java.util.Scanner(System.in);
```

**With an import:**

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
```

An import is not required when we use the fully qualified name. Imports can improve readability by avoiding repeated package names.

### 7. Explicit Import

```java
import java.util.Scanner;
```

An explicit import identifies the type being used and can make dependencies easier to understand.

### 8. Modifiers for Top-Level Classes

Top-level classes can use modifiers such as:

- `public`
- `abstract`
- `final`
- No access modifier, which gives package-private access
- `strictfp` in source code, although it is redundant in modern Java

Top-level classes **cannot** be declared `private`, `protected`, or `static`.

### 9. Modifiers for Nested Classes

Nested classes can use modifiers such as `private`, `protected`, `public`, and `static`, subject to the rules for their declaration context.

Fields, methods, and constructors also have their own permitted modifiers.

### 10. Public vs Default Access

| Modifier | Accessibility |
|---|---|
| `public` | Accessible wherever the type and its enclosing types are accessible |
| No modifier (package-private) | Accessible only within the same package |

**Important:** Default access is not the same as the `default` keyword used in other Java contexts, such as interface default methods or switch labels.

---

## Quick Interview Revision

- **Multiple classes:** A Java source file can contain multiple top-level classes.
- **Public class:** At most one public top-level class under normal file-based compilation rules.
- **Filename:** Must match the public top-level class name.
- **No public class:** The source file can have any valid filename.
- **Class order:** Does not generally affect compilation when references are valid.
- **`java.lang`:** Available automatically.
- **Same package:** No import is needed to refer to accessible types.
- **Wildcard import:** Does not import subpackages.
- **Package declaration:** Must precede imports and type declarations.
- **Top-level access:** `public` or package-private.
- **`private`, `protected`, `static`:** Not permitted on top-level class declarations.
