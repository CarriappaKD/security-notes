# Module 3: Work with Strings and Lists

## Strings in a Security Setting

An **index** is the position number assigned to each element in a sequence — with strings, that means every individual character gets its own index, and indexing always starts at **0**.

**Strings are immutable** — once created, you can't change an individual character by reassigning it through its index. Trying to do so throws an error.

Example — indexing the device ID `"h32rb17"`:

| Character | Index |
|---|---|
| h | 0 |
| 3 | 1 |
| 2 | 2 |
| r | 3 |
| b | 4 |
| 1 | 5 |
| 7 | 6 |

### Bracket Notation

Square brackets containing an index let you pull a character out of a string:
```python
device_id = "h32rb17"
print("h32rb17"[0])
print(device_id[0])
# → h
# → h
```

**Slicing** extracts more than one character at once, using two indices separated by a colon:
```python
print("h32rb17"[0:3])
# → h32
```
The slice starts at the first index given (inclusive) but stops **one position before** the second index (exclusive) — `[0:3]` returns indices 0, 1, and 2, not 3.

### String Functions and Methods

A **method** is a function that belongs to a specific data type.

| Function/Method | What It Does |
|---|---|
| **`str()`** | Converts its input into a string — e.g., turning a numeric ID into a string so it can be sliced/searched |
| **`len()`** | Returns the number of elements (characters, for a string) in an object |
| **`.upper()`** | Returns a copy of the string in all uppercase |
| **`.lower()`** | Returns a copy of the string in all lowercase |
| **`.index()`** | Returns the position of the **first** occurrence of a given character/substring; errors out if nothing matches |

```python
# str()
string_id = str(19329302)

# len() — e.g., validating a device ID is the expected length
device_id_length = len("h32rb17")
if device_id_length == 7:
    print("The device ID has 7 characters.")
# → The device ID has 7 characters.

# .upper() / .lower()
"Information Technology".upper()   # → "INFORMATION TECHNOLOGY"
"Information Technology".lower()   # → "information technology"

# .index() — first occurrence of "r"
print("h32rb17".index("r"))
# → 3
```

**Finding substrings with `.index()`:** A **substring** is any continuous run of characters within a larger string (e.g., `"llo"` inside `"hello"`). `.index()` works the same way for multi-character substrings — it returns where the match *starts*:
```python
tshah_index = "tsnow, tshah, bmoreno - updated".index("tshah")
print(tshah_index)
# → 7
```
If a character or substring shows up more than once, `.index()` only ever returns the position of the **first** match.

## Lists in a Security Setting

A list can hold multiple elements — of mixed data types, if needed — in one variable, written with square brackets and comma separation. In security contexts, lists are a natural fit for things like usernames, IP addresses, URLs, device IDs, or collections of raw data.

Like strings, list elements are indexed starting at 0:

| Element | Index |
|---|---|
| "elarson" | 0 |
| "fgarcia" | 1 |
| "tshah" | 2 |
| "sgilmore" | 3 |

**List concatenation** — merging two lists end-to-end — uses `+`.

### Bracket Notation on Lists

Same mechanics as strings:
```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print(username_list[2])
print(["elarson", "fgarcia", "tshah", "sgilmore"][2])
# → tshah
# → tshah
```

**Slicing a list** returns a **sublist** (a list that's part of the original):
```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print(username_list[0:2])
# → ['elarson', 'fgarcia']
```
Same exclusive-upper-bound rule as string slicing — index 2 ("tshah") isn't included.

### Changing List Elements

Unlike strings, lists **are** mutable — bracket notation can reassign an element directly:
```python
username_list = ["elarson", "fgarcia", "tshah", "sgilmore"]
print("Before changing an element:", username_list)
username_list[1] = "bmoreno"
print("After changing an element:", username_list)
# Before: ['elarson', 'fgarcia', 'tshah', 'sgilmore']
# After:  ['elarson', 'bmoreno', 'tshah', 'sgilmore']
```

### List Methods

| Method | Parameters | Effect |
|---|---|---|
| **`.insert()`** | index, element | Inserts the element at that index; everything from that point shifts one position later |
| **`.remove()`** | element | Removes the **first** matching occurrence of that element; everything after it shifts one position earlier |
| **`.append()`** | element | Adds the element to the **end** of the list |
| **`.index()`** | element | Returns the index of the element's first occurrence |

```python
# .insert() — adds "wjaffrey" at index 2
username_list = ["elarson", "bmoreno", "tshah", "sgilmore"]
username_list.insert(2, "wjaffrey")
# → ['elarson', 'bmoreno', 'wjaffrey', 'tshah', 'sgilmore']

# .remove() — only removes the first "elarson" if there were duplicates
username_list = ["elarson", "bmoreno", "wjaffrey", "tshah", "sgilmore"]
username_list.remove("elarson")
# → ['bmoreno', 'wjaffrey', 'tshah', 'sgilmore']

# .append() — adds to the end
username_list = ["bmoreno", "wjaffrey", "tshah", "sgilmore"]
username_list.append("btang")
# → ['bmoreno', 'wjaffrey', 'tshah', 'sgilmore', 'btang']

# .index() — position of "tshah"
username_list = ["bmoreno", "wjaffrey", "tshah", "sgilmore", "btang"]
print(username_list.index("tshah"))
# → 2
```

**`.append()` + `for` loop — a common pattern for building up a list from nothing:**
```python
numbers_list = []
for i in range(10):
    numbers_list.append(i)
print(numbers_list)
# → [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Algorithm Fundamentals

An **algorithm** is a structured set of rules or steps that takes an input, performs specific tasks on it, and produces an output to solve a problem.

Designing one gets easier when you **break a complex task into smaller, simpler pieces** — for example, working out the logic for a single item first, then extending it to process a whole collection of items.

## Regular Expressions (Regex)

A **regular expression (regex)** is a character sequence that defines a search pattern — used in Python to efficiently find structured data like IP addresses, email addresses, or device IDs inside larger strings. Regex functionality lives in the `re` module, so it needs importing first: `import re`.

### `re.findall()`

Returns a list of every match to a given pattern. Takes two parameters: the regex pattern (as a string), and the string to search through.

```python
import re
re.findall("ts", "tsnow, tshah, bmoreno")
# → ['ts', 'ts']
```
A plain alphanumeric pattern like `"ts"` just matches that literal sequence wherever it appears.

### Symbols That Match a Character Type

| Symbol | Matches | Example |
|---|---|---|
| `\w` | Any alphanumeric character (A–z, 0–9) or underscore | In `"ID_A17"`: I, D, _, A, 1, 7 |
| `\d` | Any single digit | In `"ID_A17"`: 1, 7 |
| `\s` | Any whitespace (space, tab, newline) | The space in `"user 1"` |
| `.` | Any character except a newline | — |
| `\.` | A literal period (`.`) — the backslash escapes its special meaning | — |

```python
import re
re.findall("\w", "h32rb17")   # → ['h', '3', '2', 'r', 'b', '1', '7']
re.findall("\d", "h32rb17")   # → ['3', '2', '1', '7']
```

### Symbols That Quantify Occurrences

Placed *after* a character or character-type symbol to control how many repetitions count as a match:

| Symbol | Meaning | Example |
|---|---|---|
| `+` | One or more occurrences | `\d+` matches `1`, `12`, `12345` |
| `*` | Zero, one, or more occurrences | — |
| `{n}` | Exactly *n* occurrences | `\d{4}` matches 4 consecutive digits |
| `{m,n}` | Between *m* (min) and *n* (max) occurrences | `\d{1,3}` matches `1`, `12`, or `123` |

```python
import re

re.findall("\d+", "h32rb17")
# → ['32', '17']   (groups consecutive digits together)

re.findall("\d*", "h32rb17")
# → ['', '32', '', '', '17', '']   (also matches zero digits → empty strings)

re.findall("\d{2}", "h32rb17 k825t0m c2994eh")
# → ['32', '17', '82', '29', '94']   (only exact pairs — leftover single digits are skipped)

re.findall("\d{1,3}", "h32rb17 k825t0m c2994eh")
# → ['32', '17', '825', '0', '299', '4']   (greedy within the 1–3 range)
```

**Why the `{2}` output looks the way it does:** Python scans left to right. When it finds a digit, it checks whether the *next* character is also a digit. If so, it grabs both as a pair and moves past them. If not, it just moves on without counting that lone digit at all — which is why `"825"` only yields `'82'` (the trailing `5` has no second digit to pair with).

### Constructing a Pattern from Scratch

Building a regex means breaking the target data down into its component parts and representing each part with the right symbol.

**Example:** given a string of employee records —
```python
employee_logins_string = "1001 bmoreno: 12 Marketing 1002 tshah: 7 Human Resources 1003 sgilmore: 5 Finance"
```
— the goal is to pull out just each **username + login count** pair, skipping the employee ID and department. Breaking that down:

| Piece | Regex Symbol |
|---|---|
| Username (variable-length word) | `\w+` |
| Colon | `:` |
| Space | `\s` |
| Login count (variable-length digits) | `\d+` |

Combined pattern: `"\w+:\s\d+"`
```python
import re
pattern = "\w+:\s\d+"
print(re.findall(pattern, employee_logins_string))
# → ['bmoreno: 12', 'tshah: 7', 'sgilmore: 5']
```

## Questions / Things to Revisit

-

---
*Notes based on Google Cybersecurity Professional Certificate, Course 7 — Automate Cybersecurity Tasks with Python*
