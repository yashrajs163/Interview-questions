# Interview-questions

Below are four small Python snippets you can use in your interview—each asks the candidate to predict the output and explain why. These go a step beyond simple `if` nesting and expose them to some of Python’s quirks.

---

### 1. `for`/`else` with `break`

```python
for i in range(5):
    if i == 3:
        print("Found 3")
        break
else:
    print("3 not found")
```

**Expected output:**
```
Found 3
```

**Why:**  
- The loop iterates `i = 0,1,2,3…`  
- When `i == 3`, it prints and hits `break`, exiting the loop.  
- The `else` clause on a `for` only runs if the loop completes **without** a `break`, so here it’s skipped.

---

### 2. Mutable default argument

```python
def append_to(element, to=[]):
    to.append(element)
    return to

print(append_to(1))
print(append_to(2))
print(append_to(3, []))
print(append_to(4))
```

**Expected output:**
```
[1]
[1, 2]
[3]
[1, 2, 4]
```

**Why:**  
- The default list `to` is created **once**, at function definition.  
- First call uses that list → `[1]`.  
- Second call (no `to` provided) reuses it → `[1,2]`.  
- Third call passes a new list `[]` → returns `[3]`.  
- Fourth call (default again) continues building the original → `[1,2,4]`.

---

### 3. `try`/`finally` with `return`

```python
def func():
    try:
        return "try block"
    finally:
        return "finally block"

print(func())
```

**Expected output:**
```
finally block
```

**Why:**  
- The `return "try block"` executes, but Python still runs the `finally` block **before** actually returning.  
- Since the `finally` also has a `return`, it **overrides** the earlier one.

---

### 4. List-of-lists “multiplication” pitfall

```python
matrix = [[0]*3]*3
matrix[0][0] = 1
print(matrix)
```

**Expected output:**
```
[[1, 0, 0],
 [1, 0, 0],
 [1, 0, 0]]
```

**Why:**  
- `[[0]*3]*3` doesn’t create three independent rows; it makes three **references** to the *same* inner list.  
- Changing `matrix[0][0]` affects every row at index 0.

---

These snippets are short but can trip up candidates who haven’t internalized Python’s behavior around loop-`else`, mutable defaults, `try/finally`, and list references. Asking them to **explain** their answer will quickly reveal whether they truly understand the language.




Here are four **basic “predict the output”** snippets—each short, self-contained, and highlighting a common Python gotcha. For each, ask the candidate to state what prints and **why**.

---

### 1. Loop `else` with no `break`

```python
for i in range(3):
    print(i)
else:
    print("Done")
```

**Expected output:**

```
0
1
2
Done
```

**Why:**

* The `for` runs through all values (0,1,2) without hitting a `break`.
* The `else` on a loop executes only if no `break` occurred.

---

### 2. Loop `else` with a `break`

```python
for ch in "hello":
    if ch == "x":
        print("Found x")
        break
else:
    print("No x found")
```

**Expected output:**

```
No x found
```

**Why:**

* The loop never sees an `"x"` character, so it completes normally.
* Since there’s no `break`, the `else` block runs.

---

### 3. Chained comparison

```python
x = 5
print(1 < x < 10)
print(1 < x and x < 10)
```

**Expected output:**

```
True
True
```

**Why:**

* Python supports chained comparisons: `1 < x < 10` is equivalent to `(1 < x) and (x < 10)`, but evaluated more efficiently (only one `x` lookup).

---

### 4. Mutable default argument

```python
def add_item(item, lst=[]):
    lst.append(item)
    return lst

print(add_item("a"))
print(add_item("b"))
print(add_item("c", []))
print(add_item("d"))
```

**Expected output:**

```
['a']
['a', 'b']
['c']
['a', 'b', 'd']
```

**Why:**

* The default list `lst` is created once at function definition.
* Calls without an explicit `lst` reuse that same list, accumulating items.
* Passing `[]` forces a new list for that call only.

---

These short snippets are great for verifying that a candidate really understands:

* **Loop/else** semantics
* **Comparison chaining**
* **Default argument evaluation**

Ask them to **explain** each line of execution to ensure they’re not just memorizing outputs.
