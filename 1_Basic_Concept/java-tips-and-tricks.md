# Java Tips & Tricks (Quick Reference)

Handy shortcuts, best practices, and common mistakes to avoid for each core Java concept.

---

## 1. Variables

- **Name variables clearly.** `studentAge` is better than `sa` or `x`.
- Use **camelCase** for variable names: `studentName`, not `StudentName` or `student_name`.
- Declare a variable only when you're about to use it — don't clutter code with unused variables.
- You can declare multiple variables of the same type in one line:
  ```java
  int a = 1, b = 2, c = 3;
  ```
- `final` makes a variable constant (unchangeable) — use it for values that should never change:
  ```java
  final double PI = 3.14159;
  ```

---

## 2. Data Types

- **Use `int` by default** for whole numbers — only use `long` if the number is bigger than ~2.1 billion.
- **Use `double` for decimals**, not `float`, unless you specifically need to save memory — `float` loses precision faster.
- Never compare `double`/`float` values with `==` — rounding errors can make `0.1 + 0.2 == 0.3` return `false`. Instead, check if the difference is very small:
  ```java
  Math.abs(a - b) < 0.0001
  ```
- `char` values use single quotes (`'A'`), `String` values use double quotes (`"A"`) — mixing these up is a common beginner error.
- `boolean` values are only ever `true` or `false` — never `0`/`1` like in some other languages.

---

## 3. Type Casting

- Going from **small → big** type (e.g., `int` → `double`) happens automatically — no need to cast.
- Going from **big → small** type (e.g., `double` → `int`) **must** be cast manually, and it **truncates** (cuts off) the decimal — it does not round:
  ```java
  int x = (int) 9.9; // x = 9, not 10
  ```
- To round instead of truncate, use `Math.round()`:
  ```java
  int x = Math.round(9.9f); // x = 10
  ```
- Casting a `String` to a number isn't done with `(int)` — use `Integer.parseInt()` instead:
  ```java
  int num = Integer.parseInt("25");
  ```

---

## 4. Operators

- `%` (modulus) is a fast way to check even/odd:
  ```java
  if (num % 2 == 0) { /* even */ }
  ```
- Integer division truncates the decimal — `7 / 2` gives `3`, not `3.5`. To get a decimal result, make one operand a `double`:
  ```java
  double result = 7 / 2.0; // 3.5
  ```
- Use `+=`, `-=`, `*=`, `/=` as shortcuts:
  ```java
  score += 10;   // same as score = score + 10;
  ```
- `&&` and `||` **short-circuit** — if the first condition already decides the result, Java skips checking the second. Handy for avoiding errors:
  ```java
  if (arr != null && arr.length > 0) { ... } // safe: won't check length if arr is null
  ```
- Don't confuse `=` (assignment) with `==` (comparison) — a classic beginner bug.

---

## 5. Strings

- Always compare String **content** with `.equals()`, never `==`.
- For case-insensitive comparison, use `.equalsIgnoreCase()`.
- Building strings in a loop? Use `StringBuilder` instead of `+` — it's much faster for many concatenations:
  ```java
  StringBuilder sb = new StringBuilder();
  for (int i = 0; i < 1000; i++) {
      sb.append(i);
  }
  String result = sb.toString();
  ```
- `.trim()` removes extra spaces from the start/end of a string — useful when handling user input.
- `.isEmpty()` and `.isBlank()` are quick checks before processing a string:
  ```java
  if (name.isBlank()) { System.out.println("Name required"); }
  ```
- `.split()` turns a string into an array — great for parsing CSV-like data:
  ```java
  String[] parts = "a,b,c".split(",");
  ```

---

## 6. Conditions

- Use `switch` instead of a long `if-else if` chain when checking one variable against many fixed values — it's cleaner and often faster.
- Never forget `break` in a `switch` (unless you intentionally want "fall-through") — missing it runs the next case too.
- For simple true/false assignments, use the **ternary operator** instead of a full `if-else`:
  ```java
  String result = (mark >= 50) ? "Pass" : "Fail";
  ```
- Order your `else if` checks from most specific to least specific (e.g., check `>= 90` before `>= 75`) — otherwise a higher grade might get caught by a lower check first.
- Avoid deeply nested `if` statements — flatten logic where possible using `&&`/`||` or early `return`.

---

## 7. Loops

- Know when to use which loop:
  - **`for`** → you know the number of repetitions.
  - **`while`** → repeats based on a condition, count unknown.
  - **`do-while`** → must run at least once.
- **Enhanced for-loop** (for-each) is cleaner when you don't need the index:
  ```java
  int[] marks = {80, 90, 75};
  for (int mark : marks) {
      System.out.println(mark);
  }
  ```
- Avoid infinite loops — always make sure the loop condition eventually becomes false (don't forget `i++`!).
- `break` exits the loop completely; `continue` just skips to the next iteration — mixing these up is a common bug source.
- Avoid changing the loop counter variable inside the loop body unless intentional — it can cause unpredictable behavior.

---

## 8. Arrays

- Array size is **fixed** once created — if you need a resizable list, use `ArrayList` instead:
  ```java
  ArrayList<Integer> list = new ArrayList<>();
  list.add(80);
  ```
- Watch out for `ArrayIndexOutOfBoundsException` — valid indexes go from `0` to `length - 1`, not `length`.
- `array.length` is a **property**, not a method — no parentheses (unlike `String.length()`).
- Use `Arrays.toString(array)` to quickly print an array's contents:
  ```java
  System.out.println(Arrays.toString(marks));
  ```
- `Arrays.sort(array)` sorts an array in place — handy for quick sorting tasks.

---

## 9. Methods

- Keep methods short and focused on **one task** — easier to read, test, and reuse.
- Use meaningful method names that describe the action: `calculateTotal()`, not `doStuff()`.
- If a method doesn't need to return anything, use `void`; if it computes a result, always `return` it rather than printing inside the method — this makes the method more reusable.
- Method **overloading** lets you have multiple methods with the same name but different parameters:
  ```java
  static int add(int a, int b) { return a + b; }
  static double add(double a, double b) { return a + b; }
  ```
- Break large programs into small methods early — it makes debugging much easier than one giant `main()`.

---

## General Best Practices

- **Indent consistently** — Java doesn't require it, but unreadable code leads to more bugs.
- Use meaningful names everywhere — for variables, methods, and classes.
- Comment *why* something is done, not *what* the obvious code already shows.
- Compile often. Don't write 100 lines before running `javac` for the first time — catch errors early.
- Read the error message carefully — Java's compiler errors usually tell you the exact line and issue.
- Practice by modifying example code yourself rather than just reading it — that's how the concepts actually stick.
