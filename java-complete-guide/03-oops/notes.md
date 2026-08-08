# Java OOP — Simple Guide

**OOP** stands for **Object-Oriented Programming** — writing code around real-world "objects."

In real life, we deal with things like: a Student, an Employee, a Bank Account, a Car, an Order, a Payment, a User. In Java, we model these using **classes** and **objects**.

---

## 1. Class

A **class** is a blueprint or template. It defines what an object *has* (its data) and what it *can do* (its actions).

For example, a `Student` should **have**: a name, age, and mark. A `Student` should be able to **do**: study, write an exam, show their details.

**Why use classes?** Without them, code becomes messy. With classes, code becomes structured, reusable, and much closer to how we think about the real world.

**Real-life example** — a school management app might have:
- `Student` class → student details
- `Teacher` class → teacher details
- `Course` class → course details
- `Fee` class → payment details

```java
class Student {
    String name;
    int age;

    void displayDetails() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student student1 = new Student();
        student1.name = "Venkatesh";
        student1.age = 25;
        student1.displayDetails();
    }
}
```
**Output:**
```
Name: Venkatesh
Age: 25
```

**Simple way to remember it:**
- Class = the *design*
- Object = the *actual thing* built from that design

Like a bike's design blueprint (class) vs. your actual Apache bike (object).

---

## 2. Object

An **object** is a real, usable instance created from a class. The class is just the plan — the object is the actual thing.

```java
Student student1 = new Student();
```

| Part | Meaning |
|------|---------|
| `Student` | Class name |
| `student1` | Object name |
| `new Student()` | Creates the object in memory |

**Why objects matter:** without creating an object, you can't actually use a class's data or methods.

**Real-life example** — in a banking app, each account is its own object with its own data:
```java
class BankAccount {
    String accountHolder;
    double balance;

    void showBalance() {
        System.out.println(accountHolder + " Balance: " + balance);
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account1 = new BankAccount();
        account1.accountHolder = "Venkatesh";
        account1.balance = 5000;

        BankAccount account2 = new BankAccount();
        account2.accountHolder = "Arun";
        account2.balance = 10000;

        account1.showBalance();
        account2.showBalance();
    }
}
```
**Output:**
```
Venkatesh Balance: 5000.0
Arun Balance: 10000.0
```
Both objects come from the same class, but hold different data.

---

## 3. Constructor

A **constructor** is a special method that runs automatically when an object is created, used to set its initial values. It must have the **same name as the class**, and it has **no return type** — not even `void`.

**Without a constructor**, you'd have to set values manually after creating the object:
```java
Student s1 = new Student();
s1.name = "Venkatesh";
s1.age = 25;
```

**With a constructor**, it's cleaner — you set values right when the object is created:
```java
Student s1 = new Student("Venkatesh", 25);
```

```java
class Student {
    String name;
    int age;

    Student(String studentName, int studentAge) {
        name = studentName;
        age = studentAge;
    }

    void displayDetails() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student student1 = new Student("Venkatesh", 25);
        student1.displayDetails();
    }
}
```
**Output:**
```
Name: Venkatesh
Age: 25
```

**Real-life example:** `Employee emp1 = new Employee(101, "Ravi", 50000);` — the employee's ID, name, and salary are all set the moment the object is created.

---

## 4. Encapsulation

**Encapsulation** means protecting data by hiding it and only allowing controlled access — achieved in Java using **private variables** with **public getter/setter methods**.

**Why it matters:** imagine if a bank balance could be changed directly:
```java
account.balance = -5000; // dangerous!
```
A balance should never be allowed to go negative like this. So we make the variable `private`, and only allow changes through controlled methods — which can include validation logic.

**Real-life examples where encapsulation matters:**
- Bank balance shouldn't be directly editable
- A PIN shouldn't be directly visible
- A password shouldn't be directly accessible
- Salary should be controlled through proper channels

```java
class BankAccount {
    private String accountHolder;
    private double balance;

    BankAccount(String accountHolder, double balance) {
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    public String getAccountHolder() {
        return accountHolder;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance = balance + amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance = balance - amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Invalid withdrawal amount");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("Venkatesh", 5000);

        System.out.println("Account Holder: " + account.getAccountHolder());
        System.out.println("Initial Balance: " + account.getBalance());

        account.deposit(2000);
        account.withdraw(1000);

        System.out.println("Final Balance: " + account.getBalance());
    }
}
```
**Output:**
```
Account Holder: Venkatesh
Initial Balance: 5000.0
Deposited: 2000.0
Withdrawn: 1000.0
Final Balance: 6000.0
```

**Key takeaway:** private variable + public methods = encapsulation.

---

## 5. Inheritance

**Inheritance** means one class can acquire the properties and methods of another class — done in Java using the `extends` keyword. It's a way to **reuse code** instead of writing it again and again.

**Real-life example:**
```
Vehicle
 ├── Bike
 ├── Car
 └── Bus
```
Shared details (like brand or fuel) can live in `Vehicle`, while specifics live in `Bike` or `Car`.

```java
class Vehicle {
    String brand = "TVS";

    void start() {
        System.out.println("Vehicle is starting");
    }
}

class Bike extends Vehicle {
    void showBikeDetails() {
        System.out.println("Bike Brand: " + brand);
    }
}

public class Main {
    public static void main(String[] args) {
        Bike bike = new Bike();
        bike.start();
        bike.showBikeDetails();
    }
}
```
**Output:**
```
Vehicle is starting
Bike Brand: TVS
```

`Bike` doesn't define `brand` or `start()` itself — it inherits them from `Vehicle`.

- `Vehicle` = **parent class** (superclass)
- `Bike` = **child class** (subclass)

**Another example** — in a company system:
```
Employee
 ├── Developer
 ├── Tester
 └── Manager
```
Shared: `name`, `employeeId`, `salary`. Specific: a Developer writes code, a Tester tests, a Manager manages the team.

---

## 6. Polymorphism

**Polymorphism** means "one thing, many forms" — the same method name behaving differently depending on context. It comes in two flavors:

### 6.1 Method Overloading
Same method name, but **different parameters**, within the **same class**.

**Real-life example:** a payment method that accepts different input types — `pay(cash)`, `pay(card)`, `pay(upi)`.

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }

    double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();

        System.out.println(calc.add(10, 20));
        System.out.println(calc.add(10, 20, 30));
        System.out.println(calc.add(10.5, 20.5));
    }
}
```
**Output:**
```
30
60
31.0
```

### 6.2 Method Overriding
The child class provides its own version of a method that already exists in the parent class.

**Real-life example:**
```
Payment
 ├── UPI Payment
 ├── Card Payment
 └── Net Banking Payment
```
All have a `pay()` method, but each processes payment differently.

```java
class Payment {
    void pay() {
        System.out.println("General payment processing");
    }
}

class UpiPayment extends Payment {
    @Override
    void pay() {
        System.out.println("Payment done using UPI");
    }
}

class CardPayment extends Payment {
    @Override
    void pay() {
        System.out.println("Payment done using Card");
    }
}

public class Main {
    public static void main(String[] args) {
        Payment payment1 = new UpiPayment();
        Payment payment2 = new CardPayment();

        payment1.pay();
        payment2.pay();
    }
}
```
**Output:**
```
Payment done using UPI
Payment done using Card
```

---

## 7. Abstraction

**Abstraction** means hiding internal complexity and showing only what's necessary.

**Real-life example:** using an ATM. You know how to insert your card, enter a PIN, and withdraw money — you *don't* know (or need to know) about server validation, account verification, or database updates happening behind the scenes. That's abstraction.

**Why it's useful:** it hides complex logic, shows only the important actions, improves security, and forces child classes to implement required behavior.

Java achieves abstraction using **abstract classes** and **interfaces**.

```java
abstract class Vehicle {
    abstract void start();

    void fuelType() {
        System.out.println("Vehicle needs fuel or power");
    }
}

class Bike extends Vehicle {
    @Override
    void start() {
        System.out.println("Bike starts with self-start button");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car starts with push button");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle bike = new Bike();
        Vehicle car = new Car();

        bike.start();
        bike.fuelType();

        car.start();
        car.fuelType();
    }
}
```
**Output:**
```
Bike starts with self-start button
Vehicle needs fuel or power
Car starts with push button
Vehicle needs fuel or power
```

`abstract void start();` has no body — every child class **must** provide its own implementation. `Vehicle` says "every vehicle must be able to start"; `Bike` and `Car` each decide *how*.

---

## 8. Interface

An **interface** is like a rulebook or contract — it defines *what* methods a class must have, without saying *how* they should work.

**Why it's useful:** it enables abstraction, defines shared rules across unrelated classes, supports a form of multiple inheritance, and keeps code loosely coupled.

**Real-life example:**
```
Payment interface
 ├── UpiPayment
 ├── CardPayment
 └── NetBankingPayment
```
Every payment type must have a `pay()` method, but each implements it differently.

```java
interface Payment {
    void pay(double amount);
}

class UpiPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using UPI");
    }
}

class CardPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using Card");
    }
}

public class Main {
    public static void main(String[] args) {
        Payment payment1 = new UpiPayment();
        Payment payment2 = new CardPayment();

        payment1.pay(500);
        payment2.pay(1000);
    }
}
```
**Output:**
```
Paid 500.0 using UPI
Paid 1000.0 using Card
```

### Abstract Class vs Interface

| Point | Abstract Class | Interface |
|-------|-----------------|-----------|
| Meaning | Partial abstraction | Full contract/rule |
| Keyword | `abstract class` | `interface` |
| Used by class via | `extends` | `implements` |
| Methods | Can mix abstract & normal methods | Mostly abstract (default/static allowed too) |
| Variables | Can have regular instance variables | Variables are `public static final` by default |
| Multiple support | A class can extend only one abstract class | A class can implement many interfaces |
| Best used for | A shared base among closely related classes | A shared ability across unrelated classes |

Use an **abstract class** when classes are strongly related (`Vehicle → Bike, Car`).
Use an **interface** when unrelated classes just need the same ability (`Payable → UpiPayment, CardPayment, WalletPayment`).

---

## Complete Real-World Example: Employee Salary System

This single example ties together **class, object, constructor, encapsulation, inheritance, polymorphism, abstraction, and interface**.

```java
interface BonusEligible {
    double calculateBonus();
}

abstract class Employee {
    private int id;
    private String name;
    private double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getSalary() {
        return salary;
    }

    abstract void work();

    void displayDetails() {
        System.out.println("Employee ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}

class Developer extends Employee implements BonusEligible {

    Developer(int id, String name, double salary) {
        super(id, name, salary);
    }

    @Override
    void work() {
        System.out.println(getName() + " is writing Java code");
    }

    @Override
    public double calculateBonus() {
        return getSalary() * 0.10;
    }
}

class Tester extends Employee implements BonusEligible {

    Tester(int id, String name, double salary) {
        super(id, name, salary);
    }

    @Override
    void work() {
        System.out.println(getName() + " is testing application");
    }

    @Override
    public double calculateBonus() {
        return getSalary() * 0.08;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp1 = new Developer(101, "Venkatesh", 60000);
        Employee emp2 = new Tester(102, "Arun", 50000);

        emp1.displayDetails();
        emp1.work();

        BonusEligible bonus1 = (BonusEligible) emp1;
        System.out.println("Bonus: " + bonus1.calculateBonus());

        System.out.println("----------------");

        emp2.displayDetails();
        emp2.work();

        BonusEligible bonus2 = (BonusEligible) emp2;
        System.out.println("Bonus: " + bonus2.calculateBonus());
    }
}
```

**Output:**
```
Employee ID: 101
Name: Venkatesh
Salary: 60000.0
Venkatesh is writing Java code
Bonus: 6000.0
----------------
Employee ID: 102
Name: Arun
Salary: 50000.0
Arun is testing application
Bonus: 4000.0
```

**How each concept is used here:**

| Concept | Where in the code | Purpose |
|---------|-------------------|---------|
| Class | `Employee`, `Developer`, `Tester` | Defines the model/structure |
| Object | `emp1`, `emp2` | Actual employee instances |
| Constructor | `Developer(101, "Venkatesh", 60000)` | Sets initial values |
| Encapsulation | `private id`, `private name`, `private salary` | Protects the data |
| Inheritance | `Developer extends Employee` | Reuses shared employee code |
| Polymorphism | `Employee emp1 = new Developer()` | Same parent type, different child behavior |
| Abstraction | `abstract class Employee` | Hides shared structure, forces `work()` to be defined |
| Interface | `BonusEligible` | Enforces a rule for bonus calculation |

---

## OOP Quick Summary

| Concept | Simple Meaning | Main Purpose |
|---------|-----------------|---------------|
| Class | Blueprint/template | Define structure |
| Object | Real instance | Use the class's data and methods |
| Constructor | Object initializer | Set values when the object is created |
| Encapsulation | Data hiding | Protect variables |
| Inheritance | Parent–child relationship | Reuse code |
| Polymorphism | Many forms | Same method, different behavior |
| Abstraction | Hides internal details | Show only what's necessary |
| Interface | Contract/rule | Enforce shared behavior |

---
---

# Related Java Class Concepts

## 1. Class Attributes

A **class attribute** is a variable declared inside a class — it represents an object's data/state.

```java
class Student {
    String name;
    int age;
}
```

| Attribute | Meaning |
|-----------|---------|
| `name` | Student's name |
| `age` | Student's age |

**Real-life examples:**
- A student: `name`, `age`, `rollNumber`, `mark`
- A bank account: `accountNumber`, `accountHolder`, `balance`

```java
class Student {
    String name;
    int age;
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Venkatesh";
        s1.age = 25;

        System.out.println(s1.name);
        System.out.println(s1.age);
    }
}
```
**Output:**
```
Venkatesh
25
```

---

## 2. Class Methods

A **method** is a function inside a class — it represents an object's behavior/actions.

```java
class Student {
    void study() {
        System.out.println("Student is studying");
    }
}
```

**Real-life examples:**
- A student: `study()`, `writeExam()`, `displayDetails()`
- A bank account: `deposit()`, `withdraw()`, `checkBalance()`

```java
class Student {
    String name;
    int age;

    void displayDetails() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Venkatesh";
        s1.age = 25;
        s1.displayDetails();
    }
}
```
**Output:**
```
Name: Venkatesh
Age: 25
```

---

## 3. The `this` Keyword

`this` refers to the **current object**. It's mostly used when a local variable and a class attribute share the same name.

**Problem without `this`:**
```java
class Student {
    String name;

    Student(String name) {
        name = name; // confusing — which "name" is which?
    }
}
```

**Correct way with `this`:**
```java
class Student {
    String name;

    Student(String name) {
        this.name = name;
    }
}
```

| Code | Meaning |
|------|---------|
| `this.name` | The class's attribute |
| `name` | The constructor's parameter |

**`this` is used to:**
- Refer to the current object's variable
- Resolve naming conflicts
- Call another constructor in the same class
- Call a method in the same class

```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void displayDetails() {
        System.out.println("Name: " + this.name);
        System.out.println("Age: " + this.age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Venkatesh", 25);
        s1.displayDetails();
    }
}
```
**Output:**
```
Name: Venkatesh
Age: 25
```

---

## 4. Java Modifiers

Modifiers are keywords that control access to and behavior of classes, variables, and methods. There are two types.

### 4.1 Access Modifiers
Control **where** something can be accessed from:

| Modifier | Meaning |
|----------|---------|
| `public` | Accessible from anywhere |
| `private` | Accessible only within the same class |
| `protected` | Accessible within the same package and by child classes |
| *(default)* | Accessible only within the same package |

```java
class BankAccount {
    private double balance = 5000;

    public double getBalance() {
        return balance;
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        System.out.println(account.getBalance());
    }
}
```
**Output:** `5000.0`

Since `balance` is `private`, we access it through the public `getBalance()` method.

### 4.2 Non-Access Modifiers
Change **behavior** rather than access:

| Modifier | Meaning |
|----------|---------|
| `static` | Belongs to the class itself, not to any one object |
| `final` | Cannot be changed once set |
| `abstract` | An incomplete method/class that must be implemented |
| `synchronized` | Used in multithreading |
| `volatile` | Used in multithreading |

As a beginner, focus mainly on `static`, `final`, and `abstract`.

```java
public class Main {
    public static void main(String[] args) {
        final int maxMarks = 100;
        System.out.println(maxMarks);
    }
}
```
**Output:** `100` — and this value can never be reassigned.

---

## 5. Java Packages

A **package** is like a folder that groups related Java classes together.

**Why use packages?**
- Keeps classes organized
- Avoids naming conflicts
- Lets you reuse Java's built-in classes
- Keeps large projects clean

**Real-life example** — a typical Spring Boot project layout:
```
com.example.project.controller
com.example.project.service
com.example.project.repository
com.example.project.model
```
Each package has a distinct responsibility.

Java also ships with many ready-made classes in built-in packages, e.g.:
```java
import java.util.Scanner;
```
`Scanner` here comes from the `java.util` package.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.println("Hello " + name);
    }
}
```
**Output:**
```
Enter your name: Venkatesh
Hello Venkatesh
```

---

## 6. The `super` Keyword

`super` refers to the **parent class**, and is used inside a child class.

**`super` is used to:**
- Call the parent class's constructor
- Call the parent class's method
- Access the parent class's variable

**Example:** `Employee` is the parent, `Developer` is the child — `Developer` can reuse `Employee`'s details via `super`.

```java
class Employee {
    String name;

    Employee(String name) {
        this.name = name;
    }

    void displayName() {
        System.out.println("Employee Name: " + name);
    }
}

class Developer extends Employee {
    String skill;

    Developer(String name, String skill) {
        super(name);
        this.skill = skill;
    }

    void displayDetails() {
        super.displayName();
        System.out.println("Skill: " + skill);
    }
}

public class Main {
    public static void main(String[] args) {
        Developer dev = new Developer("Venkatesh", "Java");
        dev.displayDetails();
    }
}
```
**Output:**
```
Employee Name: Venkatesh
Skill: Java
```

**`this` vs `super`:**

| Keyword | Refers to |
|---------|-----------|
| `this` | The current class's object |
| `super` | The parent class's object |

---

## 7. Inner Classes

A class declared **inside another class** is called an inner class.

```java
class Outer {
    class Inner {
        // ...
    }
}
```

**When to use it:** when one class is tightly bound to another. For example, a `Car` has an `Engine` — the `Engine` only really makes sense in the context of a `Car`, so it can be an inner class.

```java
class Car {
    String brand = "Toyota";

    class Engine {
        void start() {
            System.out.println(brand + " engine started");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        Car.Engine engine = car.new Engine();
        engine.start();
    }
}
```
**Output:** `Toyota engine started`

---

## 8. Anonymous Classes

An **anonymous class** is a class without a name — created for one-time use, usually to implement an interface or abstract class on the spot.

**Commonly used for:** event handling, callbacks, and quick implementations (though modern Java often uses lambdas instead).

```java
interface Greeting {
    void sayHello();
}

public class Main {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() {
            public void sayHello() {
                System.out.println("Hello from anonymous class");
            }
        };

        greeting.sayHello();
    }
}
```
**Output:** `Hello from anonymous class`

Normally you'd create a separate named class (`class EnglishGreeting implements Greeting {...}`) — an anonymous class skips that step entirely.

---

## 9. Enum

An **enum** defines a fixed, predefined set of constant values.

**Real-life examples:**
- `PaymentStatus`: `SUCCESS`, `FAILED`, `PENDING`
- `OrderStatus`: `PLACED`, `SHIPPED`, `DELIVERED`, `CANCELLED`
- `WeekDay`: `MONDAY`, `TUESDAY`, `WEDNESDAY`, ...
- `UserRole`: `ADMIN`, `USER`, `MANAGER`

```java
enum OrderStatus {
    PLACED,
    SHIPPED,
    DELIVERED,
    CANCELLED
}

public class Main {
    public static void main(String[] args) {
        OrderStatus status = OrderStatus.SHIPPED;
        System.out.println("Order Status: " + status);
    }
}
```
**Output:** `Order Status: SHIPPED`

**Why it matters:** enums prevent inconsistent/invalid values. Instead of risking typos like `"sucess"`, `"Successfull"`, or `"done"`, only the exact predefined values are allowed:
```java
enum PaymentStatus {
    SUCCESS,
    FAILED,
    PENDING
}
```

---

## 10. Getting User Input

To get input from the user while a program is running, Java typically uses the `Scanner` class.

**Real-life examples:** a login username, an ATM PIN, a student's mark, a product quantity, a search term.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your age: ");
        int age = scanner.nextInt();

        System.out.println("Your age is: " + age);
    }
}
```
**Output:**
```
Enter your age: 25
Your age is: 25
```

**Common Scanner methods:**

| Method | Used for |
|--------|----------|
| `nextInt()` | Reading a whole number |
| `nextDouble()` | Reading a decimal number |
| `nextLine()` | Reading a full line of text |
| `next()` | Reading a single word |
| `nextBoolean()` | Reading true/false |

---

## 11. Working with Dates

Modern Java handles dates and times through the `java.time` package.

| Class | Used for |
|-------|----------|
| `LocalDate` | Date only |
| `LocalTime` | Time only |
| `LocalDateTime` | Date and time together |
| `DateTimeFormatter` | Formatting dates/times |

**Real-life examples:** order date, payment date, invoice date, joining date, expiry date, booking date.

**Getting today's date:**
```java
import java.time.LocalDate;

public class Main {
    public static void main(String[] args) {
        LocalDate today = LocalDate.now();
        System.out.println("Today Date: " + today);
    }
}
```
**Output** (will vary based on the actual current date):
```
Today Date: 2026-06-28
```

**Creating a specific date:**
```java
import java.time.LocalDate;

public class Main {
    public static void main(String[] args) {
        LocalDate joiningDate = LocalDate.of(2026, 7, 1);
        System.out.println("Joining Date: " + joiningDate);
    }
}
```
**Output:** `Joining Date: 2026-07-01`

---

## 12. Practice Challenge

Try building this yourself to test what you've learned about class, object, attributes, methods, constructors, `this`, and encapsulation:

> Create an `Employee` class with `id`, `name`, `salary`, and a `displayDetails()` method.

**Sample solution:**
```java
class Employee {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    void displayDetails() {
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Salary: " + salary);
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee(101, "Venkatesh", 60000);
        emp.displayDetails();
    }
}
```
**Output:**
```
ID: 101
Name: Venkatesh
Salary: 60000.0
```