# Module 1: Introduction to Python

## What Is Programming?

**Programming** is how you give a computer a specific set of instructions to carry out a task. Under the hood, those instructions get converted into binary (0s and 1s) that the CPU can actually execute — each instruction maps to a concrete operation, like adding two numbers or pulling a value from memory. Higher-level languages like Python exist so humans don't have to write at that level — they let you express complex logic with far less syntax.

**Python** is a general-purpose language, usable for web development, data analysis, and automation alike. Python code has to pass through an **interpreter** first — a program that translates it into runnable instructions one line at a time. **Syntax** is the set of rules for what counts as valid, correctly structured code in a given language.

## Why Python Matters in Cybersecurity

Python's biggest use case in security work is **automation** — using technology to cut down the manual, repetitive effort involved in common tasks. Areas where it typically gets used:

- Log analysis
- Malware analysis
- Access control list management
- Intrusion detection
- Compliance checks
- Network scanning

## Where You Can Run Python

| Environment | What It Is |
|---|---|
| **Notebooks** | An online interface for writing, storing, running, and documenting code. Content lives in either a **code cell** (write/run code, usually via a play button, with output shown below it) or a **markdown cell** (formatted text describing the code, using markdown syntax — e.g., heading styles). Jupyter Notebook and Google Colab are the two most common notebook platforms, and both support multiple languages beyond just Python. |
| **IDE (Integrated Development Environment)** | A full application for writing code, with a GUI plus built-in editing assistance and error-checking tools, letting you customize your setup. |
| **Command line** | Lets you run Python directly from the terminal — you can navigate your file system, open a file editor, create new Python files, and execute them from here. |

## Data Types

A **data type** categorizes what kind of value you're working with.

| Type | Description | Quoted? | Examples |
|---|---|---|---|
| **String** | An ordered sequence of characters (letters, numbers, symbols, spaces) | Yes — single or double quotes | `"updates needed"`, `"35"`, `""` (empty string) |
| **List** | An ordered, changeable collection of elements of any type(s), in `[ ]` | No (elements may individually be quoted if strings) | `[12, 36, 54]`, `["eraab", "arusso"]`, `[]` (empty list) |
| **Integer** | A whole number, no decimal point | No | `-12`, `0`, `500` |
| **Float** | A number with a decimal point | No | `-2.2`, `0.0`, `0.34` |
| **Boolean** | Only `True` or `False` | No | `True`, `False` |
| **Tuple** | Like a list, but **immutable** — its elements can't be changed once set. In `( )` | No | `("wjaffrey", "arutley", "dkot")` |
| **Dictionary** | A set of **key-value pairs**, each key mapped to a value, separated by `:`, in `{ }` | Keys/values individually, depending on type | `{1: "East", 2: "West"}` |
| **Set** | An unordered collection of **unique** values — no duplicates allowed. In `{ }` | Depends on type | `{"jlanksy", "drosas", "nmason"}` |

**Why immutability matters for security:** A tuple's "can't be changed" property is genuinely useful in a security context — e.g., storing a list of approved software identifiers in a tuple guarantees that list can't be accidentally or maliciously altered later, so an access control list built from it stays reliable. Tuples are also more memory-efficient than lists, which matters at scale.

**`print()`** displays any of these data types, and can also evaluate expressions directly:
```python
print("updates needed")   # → updates needed
print(5 + 2)                # → 7
print(1 / 4)                 # → 0.25  (division always returns a float)
print(1 // 4)                # → 0    (floor/integer division — drops the decimal)
print(9 > 10)                # → False (comparisons return a Boolean)
```

## Variables

A **variable** is a named container that stores a value in memory, typed as one of the data types above. The value it holds can be reassigned at any time — the variable name itself doesn't change:

```python
# Assign
username = "nzhao"

# Reassign — same variable, new value
username = "zhao2"

# Assign a variable to another variable
old_username = username
```

### Naming Rules (Required)

- Only letters, numbers, and underscores (e.g., `date_3`, `username`, `interval2`)
- Case-sensitive — `time`, `Time`, `TIME`, and `timE` are all different variables
- Never use Python's reserved keywords/function names (`True`, `False`, `if`, etc.)

### Naming Style (Best Practice)

- Separate words with underscores: `login_attempts`, `invalid_user`
- Avoid near-identical names that invite confusion: `start_time` vs. `starting_time`
- Keep names reasonably short — don't write `variable_that_equals_3`
- Names should describe the data, not be arbitrary: `num_login_attempts`, `device_id`
- Alternative convention (less common in this course): **camelCase** — e.g., `loginAttempt`

## Conditional Statements

A **conditional statement** checks whether a condition evaluates to `True` or `False`, and only runs its code when the condition is met.

| Operator | Meaning |
|---|---|
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |
| `==` | equal to |
| `!=` | not equal to |

`==` and `!=` also work for comparing strings, not just numbers.

### `if`

The required starting point of any conditional. The header ends in a colon, and the body (what runs when the condition is `True`) must be indented:

```python
if status == 200:
    print("OK")
```
Parentheses around the condition are optional (`if (status == 200):` works identically).

### `else`

Runs only when every preceding condition evaluated to `False`:

```python
if status == 200:
    print("OK")
else:
    print("check other status")
```

### `elif`

Checked only if everything before it was `False`. You can chain as many `elif`s as needed, optionally followed by a final `else`:

```python
if status == 200:
    print("OK")
elif status == 400:
    print("Bad Request")
elif status == 500:
    print("Internal Server Error")
else:
    print("check other status")
```

**Important distinction:** once an `elif` in a chain evaluates `True`, Python stops checking the rest of that chain. Separate `if` statements, by contrast, are each evaluated independently regardless of what the others returned.

## Logical Operators

Used to combine multiple conditions into one check:

| Operator | Behavior |
|---|---|
| `and` | Both sides must be `True` |
| `or` | At least one side must be `True` |
| `not` | Flips the result — `True` becomes `False` and vice versa |

```python
# and — both conditions must hold
if status >= 200 and status <= 226:
    print("successful response")

# or — only one needs to hold
if status == 100 or status == 102:
    print("informational response")

# not — inverts the combined result
if not (status >= 200 and status <= 226):
    print("check status")
```

For the `not` example: Python evaluates everything inside the parentheses first (the `and` condition), then flips that result — so the message prints whenever `status` is *outside* the 200–226 range.

## Iterative Statements (Loops)

A loop repeats a block of code, either a set number of times or until a condition stops holding.

### `for` Loops

Used to step through a known sequence (a list, a string, a range of numbers):

```python
for i in ["elarson", "bmoreno", "tshah", "sgilmore"]:
    print(i)
```

The **loop variable** (`i` here) takes on each value in the sequence, one iteration at a time, until the sequence is exhausted. The header must end in a colon; the body must be indented.

**Looping through a list:**
```python
computer_assets = ["laptop1", "desktop20", "smartphone03"]
for asset in computer_assets:
    print(asset)
```

**Looping through a string** steps through it character by character:
```python
string = "cyber"
for character in string:
    print(character)
# → c, y, b, e, r
```

**`range(start, stop, step)`** generates a sequence of numbers to loop over. The start point is inclusive; the stop point is **exclusive** (not included):
```python
for i in range(0, 5, 1):
    print(i)
# → 0, 1, 2, 3, 4   (5 itself is excluded)
```
If start is 0 and step is 1 (the defaults), you can just write `range(5)` for the same result. Any non-default start or step must be written out explicitly.

### `while` Loops

Used when the loop should continue as long as a condition stays `True`, rather than for a fixed sequence:

```python
i = 1
while i < 5:
    print(i)
    i = i + 1
# → 1, 2, 3, 4
```

Unlike a `for` loop, the loop variable is **not** declared inside the header — it has to be initialized beforehand, and updated manually inside the loop body, or the loop never ends. The header still needs a trailing colon.

**Practical example — counting login attempts (integer condition):**
```python
login_attempts = 0
while login_attempts < 5:
    print("Login attempts:", login_attempts)
    login_attempts = login_attempts + 1
```

**Practical example — Boolean condition:**
```python
count = 0
login_status = True
while login_status == True:
    print("Try again.")
    count = count + 1
    if count == 4:
        login_status = False
```
Here, the loop keeps running as long as `login_status` is `True`; once `count` hits 4 (representing the 5th attempt), the flag flips to `False` and the loop exits on its next check.

### Controlling Loops: `break` and `continue`

Both are used inside a conditional statement nested within the loop body:

| Keyword | Effect |
|---|---|
| **`break`** | Exits the loop entirely as soon as the condition is met |
| **`continue`** | Skips just that one iteration and moves to the next |

```python
computer_assets = ["laptop1", "desktop20", "smartphone03"]

for asset in computer_assets:
    if asset == "desktop20":
        break
    print(asset)
# → laptop1   (loop stops entirely once it hits "desktop20")
```

```python
for asset in computer_assets:
    if asset == "desktop20":
        continue
    print(asset)
# → laptop1, smartphone03   (just skips "desktop20", keeps going)
```

### Infinite Loops

A loop that never meets its exit condition runs forever — an **infinite loop**. If this happens unintentionally, `CTRL-C` or `CTRL-Z` stops it manually. Intentional infinite loops do show up in practice, though — e.g., a server process that needs to keep listening for and processing data continuously.

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 7 — Automate Cybersecurity Tasks with Python*
