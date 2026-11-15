# Module 2: Write Effective Python Code

## Functions

A **function** is a reusable block of code — instead of repeating the same logic across a program, you define it once and call it wherever needed. In security work this matters a lot: if you're scanning logs for failed-login patterns, for example, writing a function that takes a log as input and returns the suspicious entries means you can reuse that same logic across any number of logs, rather than rewriting the check each time.

### Built-in vs. User-Defined

| Type | Description | Example |
|---|---|---|
| **Built-in** | Already exists inside Python, callable directly | `print()` |
| **User-defined** | Written by the programmer for a specific need | Any function you write yourself |

### Defining a Function

A function definition has two parts:

**1. The header** — tells Python a function is being defined. Starts with the `def` keyword, followed by the function name, parentheses, and a trailing colon:
```python
def display_investigation_message():
```
*(Tip: name functions after what they do — it makes them much easier to recall later.)*

**2. The body** — an indented block beneath the header that defines what the function actually does:
```python
def display_investigation_message():
    print("investigate activity")
```

### Calling a Function

Once defined, you run a function ("call" it) by writing its name followed by parentheses:
```python
display_investigation_message()
```

**Watch out for self-calling functions.** If a function calls itself inside its own body without a condition that eventually stops it, that creates an infinite loop:
```python
def func1():
    func1()   # calls itself forever — no stopping condition
```

## Parameters, Arguments, and Return Statements

| Term | Meaning |
|---|---|
| **Parameter** | A variable declared in the function's header, used inside the function body |
| **Argument** | The actual value passed in when the function is called |
| **Return statement** | Sends a value back out of the function using the `return` keyword |

```python
# maximum_attempts and total_attempts are PARAMETERS
def remaining_login_attempts(maximum_attempts, total_attempts):
    print(maximum_attempts - total_attempts)

# 3 and 2 are ARGUMENTS — passed in by position:
# 3 → maximum_attempts (1st position), 2 → total_attempts (2nd position)
remaining_login_attempts(3, 2)
```

Using `return` instead of `print()` lets you capture the function's output in a variable and use it elsewhere — e.g., in a calculation or a conditional:
```python
def remaining_login_attempts(maximum_attempts, total_attempts):
    return maximum_attempts - total_attempts

remaining_attempts = remaining_login_attempts(3, 3)
if remaining_attempts <= 0:
    print("Your account is locked")
# → Your account is locked
```
`return` is a keyword, not a function — never follow it with parentheses. Also, once Python hits a `return` statement, it exits the function immediately; any code written after it inside that function never runs.

## Global vs. Local Variables

| Type | Scope | Lifetime |
|---|---|---|
| **Global** | Declared outside any function; accessible everywhere, inside or outside functions | Exists for as long as the program runs |
| **Local** | Declared inside a function (including its parameters) | Created when the function is called, deleted once it finishes |

**A function can read a global variable without redeclaring it:**
```python
username = "elarson"

def identify_user():
    print(username)

identify_user()
# → elarson
```
This works, but it's not great practice — to make `identify_user()` handle different usernames, you'd have to keep reassigning the global variable from outside the function. A **parameter** is the better way to pass different values in.

**Reusing a global variable's name inside a function creates a separate local variable with that name** — the two don't affect each other:
```python
username = "elarson"
print("1:" + username)

def greet():
    username = "bmoreno"
    print("2:" + username)

greet()
print("3:" + username)

# Output:
# 1:elarson
# 2:bmoreno
# 3:elarson
```
The global `username` stays `"elarson"` throughout — the local `username` inside `greet()` is an entirely separate variable that just happens to share the name. Because mixing global and local variables with the same name gets confusing fast, it's best avoided.

## Useful Built-in Functions

| Function | What It Does |
|---|---|
| **`print()`** | Outputs any number of comma-separated arguments to the screen |
| **`type()`** | Returns the data type of a single argument — useful for catching type-related bugs |
| **`max()` / `min()`** | Return the largest / smallest value from multiple numeric arguments, or from one iterable (e.g., a list) |
| **`sorted()`** | Returns a **new** sorted list from any iterable (list or string), ascending by default — numbers sort numerically, strings sort alphabetically. Doesn't modify the original iterable. Can't sort a list/iterable with mixed data types |

```python
# type() — often wrapped in print() to actually see the result
print(type("This is a string"))
# → <class 'str'>

# max() / min() on a list
time_list = [12, 2, 32, 19, 57, 22, 14]
print(min(time_list))   # → 2
print(max(time_list))   # → 57

# sorted() — returns a new list, leaves the original untouched
time_list = [12, 2, 32, 19, 57, 22, 14]
print(sorted(time_list))   # → [2, 12, 14, 19, 22, 32, 57]
print(time_list)           # → [12, 2, 32, 19, 57, 22, 14]  (unchanged)
```

## Modules and Libraries

| Term | Definition |
|---|---|
| **Module** | A Python file containing reusable functions, variables, classes, or other code |
| **Library** | A collection of modules, bundled together for reuse |

Using pre-written modules/libraries saves time, keeps code more readable, and avoids reinventing logic that already exists.

### The Python Standard Library

Ships with Python itself. Examples relevant to security/log work:

| Module | Used For |
|---|---|
| `re` | Pattern matching in log files |
| `csv` | Working with `.csv` files |
| `glob`, `os` | Interacting with the command line/file system |
| `time`, `datetime` | Working with timestamps |
| `statistics` | Numeric calculations — e.g., `mean()` (average) and `median()` (middle value) |

**Importing an entire module** — use `import`, then prefix every function call with the module name and a dot:
```python
import statistics
monthly_failed_attempts = [20, 17, 178, 33, 15, 21, 19, 29, 32, 15, 25, 19]
mean_failed_attempts = statistics.mean(monthly_failed_attempts)
print("mean:", mean_failed_attempts)
# → mean: 35.25

median_failed_attempts = statistics.median(monthly_failed_attempts)
print("median:", median_failed_attempts)
# → median: 20.5
```
(The 178 outlier pulls the mean up noticeably above the median — useful to notice when eyeballing login-attempt data for anomalies.)

**Importing specific functions** — use `from ... import ...`, and then call the function directly, with no module prefix needed:
```python
from statistics import mean, median
monthly_failed_attempts = [20, 17, 178, 33, 15, 21, 19, 29, 32, 15, 25, 19]
print("mean:", mean(monthly_failed_attempts))
print("median:", median(monthly_failed_attempts))
```

### External Libraries

Beyond the Standard Library, you can install third-party libraries — e.g., **Beautiful Soup (`bs4`)** for parsing HTML, or **NumPy (`numpy`)** for arrays and math. Install first, then import:
```python
%pip install numpy
import numpy
```

## Code Readability

**PEP 8** is Python's official style guide — a set of formatting conventions built on the idea that code gets read far more often than it gets written, so consistency matters for anyone maintaining it later (including future-you).

### Comments

| Type | Syntax | When to Use |
|---|---|---|
| **Single-line** | Starts with `#` | Short notes; PEP 8 recommends keeping all lines (comments included) under 79 characters |
| **Multi-line** | Either repeated `#` lines, or a **docstring** (`""" """`, not assigned to a variable) | Longer explanations — e.g., documenting a function's inputs, their types, and its output |

### Indentation

Indentation isn't optional in Python — it's how the interpreter knows where a block of code (a function body, a loop body, a conditional body) starts and ends. PEP 8's standard is **4 spaces per indent level**. Nested structures stack: a conditional inside a `while` loop would have the loop body indented 4 spaces, and the conditional's body indented a further 4 spaces (8 total).

### Common Syntax Errors to Watch For

- **String data** needs quotation marks: `username = "bmoreno"`
- **Integers, floats, and Booleans** should *not* be quoted: `login_attempts = 5`, `percentage_successful = .8`, `login_status = True`
- **Lists** go in brackets, elements comma-separated: `username_list = ["bmoreno", "tshah"]`
- **Headers** (for conditionals, loops, and function definitions) must always end with a colon

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 7 — Automate Cybersecurity Tasks with Python*
