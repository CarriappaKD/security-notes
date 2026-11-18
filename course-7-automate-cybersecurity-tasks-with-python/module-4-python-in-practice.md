# Module 4: Python in Practice

## Automating Security Tasks with Python

Three typical scenarios where an analyst would use Python to enforce a control or spot suspicious activity:

| Scenario | How Python Helps |
|---|---|
| **Enforcing login timeout policies** | Track the time between a user entering their username and supplying the correct password; if it exceeds a threshold (e.g., three minutes), lock them out automatically — limits password guessing and brute-force attempts |
| **Analyzing anomalous login behavior** | Evaluate login timestamps, IP addresses, and geographic locations; flag irregular patterns like early-morning logins, access from unauthorized locations, or simultaneous connections from two different IPs |
| **Parsing log files for repeated failures** | Parse text log files (usernames, IPs, timestamps, authentication status) and use conditional logic to flag users exceeding a failure threshold in a short window (e.g., more than 3 failures in 30 minutes) |

## Automating Security in CI/CD Pipelines (DevSecOps)

**DevSecOps** (Development, Security, Operations) means building security checks directly into how software is built and released, making security a shared responsibility handled at every stage of the pipeline rather than bolted on at the end. Python fits well here because it's flexible and has a large ecosystem of libraries.

### Why Automate It

| Benefit | Why It Matters |
|---|---|
| **Speed and efficiency** | Scripted checks run fast, keeping releases quick without skipping security |
| **Finding problems early** | Issues caught during development are cheaper and easier to fix |
| **Consistency** | The same checks run the same way every build, reducing human error |
| **Lighter workload for security teams** | Frees them from repetitive work to focus on bigger problems and better automation |
| **Security culture** | Embedding checks in the pipeline makes security everyone's concern, not just the security team's |

### Tasks Python Can Automate in CI/CD

| Task | What Python Does |
|---|---|
| **SAST** (Static Application Security Testing) | Launches SAST tools that scan source code for weaknesses before it's built; interprets results, generates reports, and can halt the pipeline if serious issues are found |
| **DAST** (Dynamic Application Security Testing) | Runs DAST tools against software running in a test environment, then reads results and feeds them back into the pipeline |
| **SCA** (Software Composition Analysis) | Works with SCA tools to check dependencies (open-source code, third-party components) for vulnerabilities; controls the process, reports problems, and sets rules based on severity |
| **Vulnerability scanning** | Schedules scans of container images, infrastructure settings, and the pipeline itself; collects results and sends alerts on new findings |
| **Compliance checks** | Verifies code follows secure coding rules and infrastructure meets security guidelines; produces compliance reports |
| **Secrets management** | Scans code to stop credentials from being hardcoded; integrates with tools like HashiCorp Vault to safely retrieve and inject secrets during automated releases |
| **Policy enforcement** | Pairs with "Policy as Code" — defines policies, checks pipeline steps against them, and can automatically block a release if policies are violated (e.g., too many vulnerabilities) |

### How Python Connects to CI/CD Tools

Python works with popular CI/CD platforms like **Jenkins, GitLab CI, and CircleCI**:

- **Run scripts** — pipeline steps can execute Python scripts that carry out security tasks
- **API connections** — Python is well suited to calling APIs, letting scripts manage the release process, trigger jobs, retrieve build files, and kick off scans/pull results from security tools
- **Add-ons and extensions** — some CI/CD systems have extensions written in Python or that can run Python scripts easily

### Other Pipeline Tasks Python Can Handle

- **Setting up environments** — automate staging environments with secure network settings and controls
- **Code quality checks** — run linters to catch style problems and possible security errors early
- **Secure releases** — automate releases to staging/production using secure settings and secure file transfer

## Essential Python Components for Automation

| Component | Role in Automation |
|---|---|
| **Variables** | Store data so values don't need to be rewritten for every action |
| **Conditional statements** | Check conditions before acting, instead of manually evaluating each data point |
| **Iterative statements** | `for` loops repeat code over a sequence; `while` loops repeat based on a condition |
| **Functions** | Define reusable code once and call it anywhere; built-in functions save writing common logic yourself |
| **String techniques** | Bracket notation plus `str()`, `len()`, `.index()` |
| **List techniques** | Bracket notation plus `.insert()`, `.remove()`, `.append()`, `.index()` |
| **File handling** | Security data often lives in log files, so reading/writing files is core |

**Log file formats:** The two common ones are `.txt` and `.csv`. Both are plain-text files (no images or formatting like font/color). In a **`.csv`** file, values are separated by commas; a **`.txt`** file has no fixed separator format — values may be separated by spaces or other ways. Data is easy to extract from either, and both can be converted to other formats.

## Importing and Working with Files

### Opening a File

```python
with open("update_log.txt", "r") as file:
```

| Part | Role |
|---|---|
| **`with`** | Manages the file safely — handles errors and automatically closes the file when the indented block ends |
| **`open()`** | Opens the file; first parameter is the file name/path, second is the mode |
| **`as file`** | Assigns a variable (`file`) that references the opened file inside the block |
| **`:`** | Required at the end of the line |

- If the file is in the **same directory** as the Python file, the name alone is enough. Otherwise, use an **absolute file path** — the full location starting from the root directory: `open("/home/analyst/logs/access_log.txt", "r")`
- File names/paths are strings, so they need quotation marks.
- `open()` can be used without `with`, but then you must close the file yourself.

**File modes (second parameter):**

| Mode | Meaning |
|---|---|
| `"r"` | Read |
| `"w"` | Write — replaces existing contents (or creates a new file if it doesn't exist) |
| `"a"` | Append — adds to the end without deleting existing contents |

### Reading a File

`.read()` converts the file's contents into a single string:
```python
with open("update_log.txt", "r") as file:
    updates = file.read()
print(updates)
```
Once it's a string, all normal string operations (`.index()`, `len()`, etc.) work on it.

### Writing to a File

Useful for things like creating an approved-user allow list or standardizing an existing file. Open with `"w"` or `"a"`, then use `.write()` (which takes string data):
```python
line = "jrafael,192.168.243.140,4:56:27,True"
with open("access_log.txt", "a") as file:
    file.write(line)
```
- `"w"` on an existing file overwrites it; `"w"` on a new name (e.g., `"update_log2.txt"`) creates it
- `"a"` keeps existing content and adds the new string at the end
- Calling `.write()` without `with` risks incomplete writes if the file isn't closed properly

## Parsing

**Parsing** converts data into a more readable/usable format — either so Python code can process it in a particular way, or so a human can interpret the output more easily. Two key methods: `.split()` and `.join()`.

### `.split()` — String → List

Splits a string into a list at a specified separator character:
```python
approved_users = "elarson,bmoreno,tshah,sgilmore,eraab"
approved_users = approved_users.split(",")
# → ['elarson', 'bmoreno', 'tshah', 'sgilmore', 'eraab']
```
With **no argument**, it splits at any whitespace (spaces, newlines, etc.):
```python
removed_users = "wjaffrey jsoto abernard jhill awilliam"
removed_users = removed_users.split()
# → ['wjaffrey', 'jsoto', 'abernard', 'jhill', 'awilliam']
```

**Applied to files** — read the file to a string with `.read()`, then split it into a list so it can be looped over:
```python
with open("update_log.txt", "r") as file:
    updates = file.read()
updates = updates.split()
```
The `.split()` line sits outside the `with` block on purpose — the file closes as soon as it's no longer needed, which keeps code tidy.

### `.join()` — List → String

Concatenates the elements of an iterable into one string. The separator character goes *before* `.join()`, and the list is passed in as the argument:
```python
approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
approved_users = ",".join(approved_users)
# → elarson,bmoreno,tshah,sgilmore,eraab
```
Using `"\n"` as the separator puts each element on its own line.

**Applied to files** — since `.write()` only accepts strings, a list must be joined back into a string first:
```python
updates = " ".join(updates)
with open("update_log.txt", "w") as file:
    file.write(updates)
```
This rebuilds the string (space-separated) and overwrites the original file with it.

## Debugging

### Three Types of Errors

| Type | What It Is | Error Message? |
|---|---|---|
| **Syntax error** | Invalid use of the language itself — e.g., a missing closing bracket, quote, or colon | Yes — labeled `SyntaxError`, with line number and a description |
| **Logic error** | Code is valid and runs, but produces unintended results (wrong operator, wrong value, misplaced indentation) | **No** — it runs without complaint, just does the wrong thing |
| **Exception** | Syntactically correct code that can't be executed | Yes — named by type |

**Syntax errors:** the output points to the exact location. Common descriptions include "invalid syntax" or "unexpected EOF while parsing" (EOF = end of file); an unclosed string might say "EOL while scanning string literal" (EOL = end of line). `IndentationError` is a subclass of `SyntaxError` for bad indentation.
```python
message = "You are debugging a syntax error     # missing closing quote
print(message)
# → SyntaxError: EOL while scanning string literal
```

**Logic errors:** e.g., using `>=` where `<` was intended. The code below runs fine but prints the wrong message:
```python
login_attempts = 5
if login_attempts >= 5:
    print("User has not reached maximum number of login attempts.")   # wrong!
else:
    print("User has reached maximum number of login attempts.")
```

**Common exceptions:**

| Exception | Cause |
|---|---|
| `NameError` | Using a variable that hasn't been assigned, or a function that hasn't been defined |
| `IndexError` | Referencing an index that doesn't exist in the sequence (e.g., `usernames[3]` on a 3-element list) |
| `TypeError` | Using the wrong data type — e.g., adding a string to an integer |
| `FileNotFoundError` | Trying to open a file that doesn't exist at the given location |

```python
print("Unusual logins:", unusual_logins)
# → NameError: name 'unusual_logins' is not defined
```
Fix: assign `unusual_logins` a value before using it.

### Debugging Strategies

If there are multiple errors, Python reports them **one at a time**, starting with the first it hits — fix it, rerun, and it'll report the next. Syntax error messages usually point straight to the fix; logic errors and exceptions often need extra strategies.

**1. Debuggers** — tools built into many IDEs that help trace the source of an error. They use **breakpoints** (markers on specific lines that control which code runs during debugging), and many let you watch variable values change as the code executes — especially handy for tracking down logic errors. AI coding assistants inside IDEs can speed up this work too, but their output can be inaccurate, suboptimal, or insecure — always review and validate AI-generated code before running it, and treat it as a co-pilot, not the final authority.

**2. Temporary print statements** — insert `print()` calls at key points to trace which parts of the code actually run. Example: this code should only add users who aren't already approved, but a duplicate gets added anyway:
<table>
<tr>
<th>Before — no debugging prints</th>
<th>After — with debugging prints</th>
</tr>
<tr>
<td valign="top">

```python
new_users = ["sgilmore", "bmoreno"]
approved_users = ["bmoreno", "tshah", "elarson"]

def add_users():
    for user in new_users:
        if user in approved_users:
            print(user, "already in list")
        approved_users.append(user)

add_users()
print(approved_users)
```

**Output:**
```
bmoreno already in list
['bmoreno', 'tshah', 'elarson', 'sgilmore', 'bmoreno']
```

</td>
<td valign="top">

```python
new_users = ["sgilmore", "bmoreno"]
approved_users = ["bmoreno", "tshah", "elarson"]

def add_users():
    for user in new_users:
        print("line 5 - inside for loop")
        if user in approved_users:
            print("line 7 - inside if statement")
            print(user, "already in list")
        print("line 9 - before .append method")
        approved_users.append(user)

add_users()
print(approved_users)
```

**Output:**
```
line 5 - inside for loop
line 9 - before .append method
line 5 - inside for loop
line 7 - inside if statement
bmoreno already in list
line 9 - before .append method
['bmoreno', 'tshah', 'elarson', 'sgilmore', 'bmoreno']
```

</td>
</tr>
</table>

Reading the right-hand output: the `for` loop line prints twice (once per username — expected), and the `if` line prints once (only one username was already approved — also expected). But `"line 9 - before .append method"` prints **twice**, which shows the `.append()` line runs for **both** users, even the one already in the list. That isolates the bug: `approved_users.append(user)` needs to sit inside an `else` block so it only runs when the user isn't already approved.

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 7 — Automate Cybersecurity Tasks with Python*
