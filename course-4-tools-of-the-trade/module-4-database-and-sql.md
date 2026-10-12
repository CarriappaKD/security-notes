# Module 4: Databases and SQL

## Databases and Relational Databases

A **database** is an organized collection of information used to manage large datasets and support decision-making — things like login attempts, software update history, or machine ownership records.

A **relational database** organizes data into interconnected tables:

- **Columns (fields)** define the type of information stored.
- **Rows (records)** contain the individual data entries.

### Keys

| Key | Role |
|---|---|
| **Primary key** | Uniquely identifies each row in a table — no duplicates, no empty values |
| **Foreign key** | A column in one table that points to the primary key of another table, creating a relationship between the two tables |

## SQL (Structured Query Language)

**SQL** is the language used to create, interact with, and request data from a database. A **query** is a request for data from one or more tables — SQL can process millions of data points in security logs quickly to surface the relevant records.

### SQL vs. Linux Filtering

| | Linux | SQL |
|---|---|---|
| **Purpose** | Filters files/directories on a computer system — searching files, managing permissions/processes | Filters data stored in database tables |
| **Syntax** | Different tools, different syntax (`find`, `grep`, `cut`, `sed`, etc.) | One standardized language with consistent keywords (`WHERE`, `SELECT`, `JOIN`) |
| **Structure** | Free-form — output is printed as plain lines of text | Structured — data is organized into columns, making specific fields easy to isolate |
| **Joining data** | No built-in way to connect data across files | Can `JOIN` multiple tables together in one query |
| **Best use** | Useful when the data isn't in a database-compatible format, e.g. plain text log files | Best when data already lives in a structured database |

## Basic Query Keywords

Every SQL query needs at minimum **`SELECT`** and **`FROM`**. Keywords aren't case-sensitive, but uppercasing them (`SELECT`, `FROM`) is standard for readability. Every statement ends in a semicolon (`;`); line breaks are optional but make longer queries easier to read.

| Keyword | Function |
|---|---|
| `SELECT` | Specifies which columns to return. Multiple columns are comma-separated. `SELECT *` returns all columns (best avoided on very large tables) |
| `FROM` | Specifies which table to query — written after `SELECT` |
| `ORDER BY` | Sorts the returned records by a given column. Ascending by default; add `DESC` for descending. Can sort by multiple columns in sequence (e.g., country first, then city within each country) |

```sql
SELECT customerid, city, country
FROM customers
ORDER BY country, city;
```

## Filtering with WHERE

`WHERE` adds a condition to a query so only matching rows are returned.

```sql
SELECT firstname, lastname, title, email
FROM employees
WHERE title = 'IT Staff';
```

### Wildcards and the `LIKE` Operator

Pattern matching requires swapping `=` for **`LIKE`**, plus a wildcard character:

| Wildcard | Matches |
|---|---|
| `%` | Any number of characters |
| `_` | Exactly one character |

| Pattern | Could match |
|---|---|
| `'a%'` | apple123, art, a |
| `'a_'` | as, an, a7 |
| `'%a'` | pizza, Z6ra, a |
| `'%a%'` | Again, back, a |

```sql
SELECT lastname, firstname, title, email
FROM employees
WHERE title LIKE 'IT%';     -- matches 'IT Staff', 'IT Manager', etc.
```

## Common Data Types

| Type | Examples |
|---|---|
| **String** | Usernames, text fields (e.g., `"analyst10"`) |
| **Numeric** | Login attempt counts, data volume sent/received |
| **Date/time** | Login dates, login times, patch dates, connection duration |

### Comparison Operators (Numeric and Date/Time)

| Operator | Meaning |
|---|---|
| `<` | Less than |
| `>` | Greater than |
| `=` | Equal to |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `<>` or `!=` | Not equal to |

An **exclusive** operator doesn't include the comparison value itself; an **inclusive** one does.

### `BETWEEN`

Filters for a range of numbers or dates — **inclusive** of both endpoints.

```sql
WHERE OS_patch_date BETWEEN '21-03-2021' AND '21-07-2021';
```

> String, date, and time values need quotation marks in filters; numeric values don't.

## Logical Operators

| Operator | Behavior |
|---|---|
| **AND** | Both conditions must be true |
| **OR** | Either condition (or both) can be true |
| **NOT** | Negates a single condition — returns everything that *doesn't* match |

```sql
-- AND: both conditions required
SELECT firstname, lastname, email, country, supportrepid
FROM customers
WHERE supportrepid = 5 AND country = 'USA';

-- OR: either condition
SELECT firstname, lastname, email, country
FROM customers
WHERE country = 'Canada' OR country = 'USA';

-- NOT: negates a single condition
SELECT firstname, lastname, email, country
FROM customers
WHERE NOT country = 'USA';
```

`NOT country = 'USA'` is equivalent to `country <> 'USA'` or `country != 'USA'`.

### Combining Operators

```sql
SELECT firstname, lastname, email, country
FROM customers
WHERE NOT country = 'Canada' AND NOT country = 'USA';
```

## Joins

A **join** combines data from two or more tables.

| Join Type | Returns |
|---|---|
| **INNER JOIN** | Only rows where the join column matches in *both* tables |
| **LEFT JOIN** | All rows from the first (left) table, plus only matching rows from the second (right) table |
| **RIGHT JOIN** | All rows from the second (right) table, plus only matching rows from the first (left) table |
| **FULL OUTER JOIN** | All rows from *both* tables, matched where possible |

**INNER JOIN** — only matching rows from both tables:
```sql
SELECT *
FROM employees
INNER JOIN machines ON employees.device_id = machines.device_id;
```

**LEFT JOIN** — all rows from `employees` (left), matching rows from `machines` (right):
```sql
SELECT *
FROM employees
LEFT JOIN machines ON employees.device_id = machines.device_id;
```

**RIGHT JOIN** — all rows from `machines` (right), matching rows from `employees` (left):
```sql
SELECT *
FROM employees
RIGHT JOIN machines ON employees.device_id = machines.device_id;
```

**FULL OUTER JOIN** — all rows from both tables:
```sql
SELECT *
FROM employees
FULL OUTER JOIN machines ON employees.device_id = machines.device_id;
```

- The left table comes after `FROM`; the right table comes after the join keyword.
- `ON` specifies the matching column, written as `table.column` on both sides.
- If a column name exists in both tables, it must be qualified with its table name (e.g., `employees.device_id`) when using `SELECT *`, since it would otherwise be ambiguous.
- Swapping a `LEFT JOIN`'s table order produces the same result as a `RIGHT JOIN` with the original order, and vice versa.

## Aggregate Functions

Aggregate functions calculate a single summary value across multiple rows — they don't return the underlying raw data.

| Function | Returns |
|---|---|
| `COUNT(column)` | Number of records with a value in that column |
| `AVG(column)` | Average of the numeric values in that column |
| `SUM(column)` | Sum of the numeric values in that column |

```sql
SELECT COUNT(firstname)   -- how many records have a value in firstname
SELECT AVG(height)        -- average height across all records
SELECT SUM(cost)          -- total cost across all records
```

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 4 — Tools of the Trade: Linux and SQL*
