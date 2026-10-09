# Module 3: Linux Commands in the Bash Shell

## Commands and Arguments

A **command** is an instruction telling the computer to perform a specific action — finding a file, launching a program, printing text, etc. An **argument** provides the specific information a command needs to carry out that action; some commands take more than one argument. All Linux commands, arguments, file names, and directory names are **case-sensitive**.

## Filesystem Hierarchy Standard (FHS)

The FHS is the part of Linux that organizes where data lives — it defines how directories, their contents, and other storage are structured so the OS always knows where to find things. A **file path** is the location of a file or directory, with each level of the hierarchy separated by a forward slash (`/`).

### Key Directories Under Root

| Directory | Contains |
|---|---|
| `/home` | Each user's personal home directory |
| `/bin` | Binary/executable files (programs that run a sequence of commands) |
| `/etc` | System configuration files |
| `/tmp` | Temporary files — frequently targeted by attackers since any user on the system can modify data there |
| `/mnt` | Mounted media, such as USB or external hard drives |

### Absolute vs. Relative Paths

- **Absolute path** — the full path starting from root (e.g., `/home/analyst/projects`)
- **Relative path** — the path starting from the current directory. Uses `.` for "current directory" and `..` for "parent of current directory" (e.g., `../projects`)
- **`~`** — shorthand for the current user's home directory, used when a path is below it

## Navigation and Reading Commands

| Command | Function |
|---|---|
| `pwd` | Prints the absolute path of the current working directory |
| `whoami` | Returns the username of the currently logged-in user |
| `ls` | Lists files/directories in the current directory (or a given path, if supplied as an argument) |
| `cd` | Changes directory — takes a subdirectory name, an absolute path, or `..` to move up one level |
| `cat` | Prints a file's entire contents to the screen |
| `head` | Shows the first 10 lines of a file by default; use `-n` to change the line count |
| `tail` | Shows the last 10 lines of a file by default |
| `less` | Displays file contents one page at a time |

### `less` Navigation Keys

| Key | Action |
|---|---|
| Space bar | Forward one page |
| `b` | Back one page |
| ↓ | Forward one line |
| ↑ | Back one line |
| `q` | Quit, return to terminal |

## Filtering for Information

**Filtering** means narrowing results down to data that matches a specific condition — a file extension, a string of text, etc.

| Tool | Function |
|---|---|
| `grep` | Searches a given file and prints every line containing a given string. Takes two arguments: the search string, then the file. E.g., `grep error time_logs.txt` prints only lines containing "error" |
| `\|` (pipe) | Sends the output of one command into another command as its input, chaining commands together. E.g., `ls /home/analyst/reports \| grep users` lists only entries in `reports` that contain "users" |
| `find` | Searches recursively through directories for files/directories matching given criteria (name, size, modification time, etc.) |

### `find` Options

| Option | Behavior |
|---|---|
| `-name` | Matches a string in the file/directory name — **case-sensitive**. `*` is a wildcard for any characters. E.g., `find /home/analyst/projects -name "*log*"` |
| `-iname` | Same as `-name` but **case-insensitive** |
| `-mtime` | Filters by last-modified time, in days. `-mtime +1` = modified more than 1 day ago; `-mtime -1` = modified less than 1 day ago |
| `-mmin` | Same as `-mtime` but based on minutes instead of days |

`find` syntax: the first argument is *where* to start searching, followed by the criteria/options to narrow the search. Skipping criteria tends to return too much.

## Directory and File Management

| Command | Function | Example |
|---|---|---|
| `mkdir` | Creates a new directory | `mkdir /home/analyst/logs/network` |
| `rmdir` | Deletes a directory — only works if it's empty | `rmdir /home/analyst/logs/network` |
| `touch` | Creates a new, empty file | `touch permissions.txt` |
| `rm` | Deletes a file (not easily recoverable — use carefully) | `rm permissions.txt` |
| `mv` | Moves a file/directory to a new location; also used to rename (pass the new name as the second argument) | `mv permissions.txt /home/analyst/logs` |
| `cp` | Copies a file/directory to a new location, without removing the original | `cp permissions.txt /home/analyst/logs` |

### `nano` Text Editor

A default command-line editor for creating and modifying files directly in the terminal.

- Open/create a file: `nano permissions.txt`
- Save: `Ctrl + O`, then confirm the filename
- Exit: `Ctrl + X`
- No auto-save — work must be saved manually before exiting.

### Output Redirection

| Operator | Behavior | Example |
|---|---|---|
| `>` | Overwrites the target file's contents (not easily recoverable) | `echo "time" > permissions.txt` |
| `>>` | Appends to the end of the target file instead of overwriting | `echo "last updated date" >> permissions.txt` |

Both operators create the file if it doesn't already exist.

## File Permissions and Ownership

**Authorization** is granting access to resources on a need-to-know basis, to limit security risk.

### Permission Types

| Permission | On a File | On a Directory |
|---|---|---|
| **read (r)** | View file contents | List the directory's contents (files + subdirectories) |
| **write (w)** | Modify file contents | Create new files inside the directory |
| **execute (x)** | Run the file, if it's a program | Enter ("traverse") the directory and access its contents |

### Owner Types

| Owner | Meaning |
|---|---|
| **user (u)** | The file's owner |
| **group (g)** | A broader group the owner belongs to |
| **other (o)** | Everyone else on the system |

Permissions appear as a 10-character string (e.g., `drwxrwxrwx`): the first character is the file type (`d` = directory, `-` = regular file), followed by three sets of `rwx` for user, group, and other, in that order.

### Relevant `ls` Options

| Option | Shows |
|---|---|
| `ls -a` | Hidden files (names starting with `.`) |
| `ls -l` | Permissions plus owner, group, size, and last-modified time |
| `ls -la` | Both of the above combined |

### Changing Permissions with `chmod`

**Principle of least privilege**: grant only the minimum access needed to do a job — `chmod` ("change mode") is the tool for enforcing it. It takes two arguments: how to change the permissions, and which file/directory to change them on.

| Symbol | Meaning |
|---|---|
| `u` / `g` / `o` | Target: user / group / other |
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set permission exactly (overwrites whatever was there) |

Multiple owner types in one command are separated by commas, with **no spaces** after the commas.

```
chmod u+rwx,g+rwx,o+rwx login_sessions.txt   # grant all permissions to everyone
chmod u-rwx,g-rwx,o-rwx login_sessions.txt   # remove all permissions from everyone
chmod u=r,g=r,o=r login_sessions.txt         # set read-only for everyone, overwriting prior perms
```

## Root User and `sudo`

- The **root user** (superuser) has unrestricted permissions — can create, modify, or delete any file and run any program.
- Logging in directly as root is bad practice: it's a security risk, mistakes are hard to undo, and it's difficult to track who did what in a multi-user system.
- **`sudo`** ("super user do") temporarily elevates a specific user's permissions for a single command, instead of logging in as root outright. Only users listed in the **sudoers file** are allowed to use it. Because `sudo` bypasses normal access controls, it's also a high-value target if an attacker compromises a sudo-enabled account.

### User and Group Management (via `sudo`)

| Command | Function |
|---|---|
| `useradd` | Adds a new user. `-g` sets their primary group; `-G` adds them to one or more supplemental groups |
| `usermod` | Modifies an existing user. `-g`/`-G` work as above; `-a` (used with `-G`) appends a supplemental group without removing existing ones; `-d` changes home directory; `-l` changes login name; `-L` locks the account |
| `userdel` | Deletes a user. Does **not** delete their home directory unless `-r` is used — back up first. Locking an account with `usermod -L` is often safer than deleting it outright |
| `groupdel` | Removes a group — good practice after `userdel`, since a user's personal same-named group is left behind otherwise |
| `chown` | Changes ownership. User: `chown rohit access.txt`. Group (note the leading colon): `chown :security access.txt` |

**Examples:**
```
sudo useradd -g security john              # add john, primary group = security
sudo useradd -G finance,admin john         # add john to supplemental groups finance and admin
sudo usermod -g executive rahul            # change rahul's primary group to executive
sudo usermod -a -G marketing rahul         # add rahul to supplemental group marketing, keep existing groups
sudo userdel sachin                        # delete user sachin (home dir kept unless -r)
sudo groupdel sachin                       # clean up sachin's leftover personal group
```

## Getting Help

| Command | Function |
|---|---|
| `man` | Shows a command's full manual — description and all available options. E.g., `man usermod` |
| `whatis` | Gives a one-line summary of a command — useful when a full manual page is overkill |
| `apropos` | Searches manual page descriptions for a keyword; `-a` requires multiple keywords to all match. E.g., `apropos -a graph editor` |

The wider Linux community (e.g., Unix & Linux Stack Exchange) is also a reliable source for troubleshooting, since Linux's open-source nature has built up a large base of ranked, high-quality answers.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 4 — Tools of the Trade: Linux and SQL*
