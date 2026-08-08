# Java Basic Concepts (Simple Guide)

This covers the core building blocks of Java, in the order you should learn them.

---

## 1. Variables

A variable is just a **name given to a value** stored in memory.

```java
int age = 25;
String name = "Venkatesh";
double salary = 45000.50;
```

| Part | Meaning |
|------|---------|
| `int` | Data type |
| `age` | Variable name |
| `25` | Value |

**Real-life example** — storing details for a student app:
```java
String studentName = "Arun";
int studentAge = 20;
double mark = 85.5;
```

---

## 2. Data Types

A data type tells Java what *kind* of value a variable can hold.

```java
int age = 25;   // int means "age" will hold a whole number
```

| Data Type | Used For | Example |
|-----------|----------|---------|
| `int` | Whole numbers | 10, 25, 100 |
| `double` | Decimal numbers | 10.5, 99.99 |
| `char` | A single character | 'A', 'B' |
| `boolean` | True or false | true, false |
| `String` | Text | "Java" |

```java
int age = 25;
double price = 99.50;
char grade = 'A';
boolean isPassed = true;
String course = "Java";
```

---

## 3. Type Casting

Type casting means converting one data type into another.

### Automatic Casting
A smaller type converts into a bigger type automatically.
```java
int number = 10;
double result = number;

System.out.println(result);
```
**Output:** `10.0` — the `int` became a `double` on its own.

### Manual Casting
A bigger type converts into a smaller type only when you tell it to.
```java
double price = 99.99;
int finalPrice = (int) price;

System.out.println(finalPrice);
```
**Output:** `99` — the decimal part gets dropped.

---

## 4. Operators

Operators let you do things like math, comparisons, and logical checks.

### Arithmetic Operators (math)
| Operator | Meaning | Example |
|----------|---------|---------|
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Division | `a / b` |
| `%` | Remainder | `a % b` |

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a - b); // 7
System.out.println(a * b); // 30
System.out.println(a / b); // 3
System.out.println(a % b); // 1
```

### Comparison Operators
| Operator | Meaning |
|----------|---------|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

```java
int age = 18;
System.out.println(age >= 18); // true
```

### Logical Operators
| Operator | Meaning |
|----------|---------|
| `&&` | AND — both conditions must be true |
| `!` | NOT — flips the result |

```java
int age = 20;
boolean hasId = true;

System.out.println(age >= 18 && hasId == true); // true
```

---

## 5. Strings

A `String` stores text, always written in double quotes.

```java
String name = "Java";
```

### Common String Methods

| Method | Meaning |
|--------|---------|
| `length()` | Counts characters |
| `toUpperCase()` | Converts to uppercase |
| `toLowerCase()` | Converts to lowercase |
| `charAt()` | Gets a character at a specific position |
| `equals()` | Compares two strings |
| `contains()` | Checks if some text exists inside the string |

```java
String course = "Java Programming";

System.out.println(course.length());        // 16
System.out.println(course.toUpperCase());   // JAVA PROGRAMMING
System.out.println(course.toLowerCase());   // java programming
System.out.println(course.contains("Java")); // true
```

### Comparing Strings
Always use `.equals()` to compare the *value* of two strings:
```java
String name1 = "Java";
String name2 = "Java";

System.out.println(name1.equals(name2)); // true
```

⚠️ Avoid `name1 == name2` for text comparison — `==` checks whether they're the *same object in memory*, not whether the text matches.

---

## 6. Conditions

Conditions let your program make decisions.

> Example: if a mark is above 50, the student passed — otherwise, they failed.

### `if` Statement
```java
int age = 20;

if (age >= 18) {
    System.out.println("Eligible to vote");
}
```

### `if / else` Statement
```java
int mark = 40;

if (mark >= 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail"); // this runs
}
```

### `else if` Statement
```java
int mark = 85;

if (mark >= 90) {
    System.out.println("Grade A");
} else if (mark >= 75) {
    System.out.println("Grade B"); // this runs
} else if (mark >= 50) {
    System.out.println("Grade C");
} else {
    System.out.println("Fail");
}
```

### `switch` Statement
Useful when you have several fixed choices to pick from.
```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday"); // this runs
        break;
    default:
        System.out.println("Invalid day");
}
```

---

## 7. Loops

Loops repeat code without you having to write it over and over.

### `for` Loop
Use when you know exactly how many times to repeat.
```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
// Output: 1 2 3 4 5
```

### `while` Loop
Use when repetition depends on a condition, and you don't know the exact count in advance.
```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
// Output: 1 2 3 4 5
```

### `do while` Loop
Runs **at least once**, even if the condition is false from the start.
```java
int i = 1;

do {
    System.out.println(i);
    i++;
} while (i <= 5);
// Output: 1 2 3 4 5
```

### `break` and `continue`

**`break`** — stops the loop entirely:
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break;
    }
    System.out.println(i);
}
// Output: 1 2
```

**`continue`** — skips just the current step and moves to the next:
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
// Output: 1 2 4 5
```

---

## 8. Arrays

An array stores multiple values in a single variable.

Instead of this:
```java
int mark1 = 80;
int mark2 = 90;
int mark3 = 75;
int mark4 = 60;
```

You can do this:
```java
int[] marks = {80, 90, 75, 60};
```

### Accessing Array Values
Array indexes start at **0**.
```java
int[] marks = {80, 90, 75, 60};

System.out.println(marks[0]); // 80
System.out.println(marks[1]); // 90
```

| Index | Value |
|-------|-------|
| 0 | 80 |
| 1 | 90 |
| 2 | 75 |
| 3 | 60 |

### Looping Through an Array
```java
int[] marks = {80, 90, 75, 60};

for (int i = 0; i < marks.length; i++) {
    System.out.println(marks[i]);
}
// Output: 80 90 75 60
```

---

## 9. Methods

A method is a **reusable block of code** that performs a specific task.

```java
public static void greet() {
    System.out.println("Hello Java");
}
```

Call it like this:
```java
greet();
```

### Full Example
```java
public class Main {

    public static void greet() {
        System.out.println("Hello Java");
    }

    public static void main(String[] args) {
        greet();
    }
}
// Output: Hello Java
```

### Methods With Parameters
Parameters are inputs you pass into a method.
```java
public class Main {

    public static void greetUser(String name) {
        System.out.println("Hello " + name);
    }

    public static void main(String[] args) {
        greetUser("Venkatesh");
        greetUser("Arun");
    }
}
// Output:
// Hello Venkatesh
// Hello Arun
```

### Methods That Return a Value
```java
public class Main {

    public static int add(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        int result = add(10, 20);
        System.out.println(result);
    }
}
// Output: 30
```

---

## 10. Putting It All Together

Here's one program that uses variables, methods, conditions, arrays, and loops together:

```java
public class Main {

    public static int calculateTotal(int mark1, int mark2, int mark3) {
        return mark1 + mark2 + mark3;
    }

    public static void main(String[] args) {

        String studentName = "Venkatesh";
        int mark1 = 80;
        int mark2 = 75;
        int mark3 = 90;

        int total = calculateTotal(mark1, mark2, mark3);
        double average = total / 3.0;

        System.out.println("Student Name: " + studentName);
        System.out.println("Total Marks: " + total);
        System.out.println("Average: " + average);

        if (average >= 50) {
            System.out.println("Result: Pass");
        } else {
            System.out.println("Result: Fail");
        }

        int[] marks = {mark1, mark2, mark3};

        System.out.println("All Marks:");

        for (int i = 0; i < marks.length; i++) {
            System.out.println(marks[i]);
        }
    }
}
```

**Output:**
```
Student Name: Venkatesh
Total Marks: 245
Average: 81.66666666666667
Result: Pass
All Marks:
80
75
90
```

---

## Final Summary

| Concept | Simple Meaning |
|---------|-----------------|
| Variables | Store values |
| Data Types | Define the type of value |
| Type Casting | Convert one type to another |
| Operators | Perform operations |
| Strings | Store and handle text |
| Conditions | Make decisions |
| Loops | Repeat code |
| Arrays | Store multiple values |
| Methods | Reuse code |

## Correct Learning Order

```
Variables → Data Types → Type Casting → Operators
   → Strings → Conditions → Loops → Arrays → Methods
```

Once you're comfortable with these, the next step is **Object-Oriented Programming (OOP)**: Class, Object, Constructor, Encapsulation, Inheritance, Polymorphism, Abstraction, and Interface.
