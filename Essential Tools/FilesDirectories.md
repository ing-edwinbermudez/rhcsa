# Files and Directories

### **Listing Files and Directories**

Lists files and directories in the current location (excluding hidden files).

```bash
ls
```

Lists all files and directories, including hidden ones (those starting with a dot .), in long format (with permissions, ownership, size, and timestamps).


```bash
ls -la
```

### 🔍 Useful ls options

| Option | Description                                               |
| ------ | --------------------------------------------------------- |
| `-l`   | Long format (permissions, owner, size, date)              |
| `-a`   | Show all files including hidden ones (`.` files)          |
| `-h`   | Human-readable file sizes (e.g., KB, MB) — used with `-l` |
| `-t`   | Sort by modification time (newest first)                  |
| `-S`   | Sort by file size (largest first)                         |
| `-r`   | Reverse the order of the sort                             |

### Current / Working Directory

**Print Working Directory**

Prints the current working directory (i.e., where you are in the filesystem).

```bash
pwd
```

Change Directory `cd`
```bash
cd 
```

Moves up one level in the directory tree (to the parent directory).
```bash
cd ..
```

Changes to the specified absolute path /home/ehbc.

```bash
cd /home/ehbc
```

Go back to the previous directory.

```bash
cd -
```

The tree command displays directories and files in a tree-like format, showing the hierarchical structure of the filesystem.

```bash
tree
```

| Option       | Description                                     |
| ------------ | ----------------------------------------------- |
| `-L [level]` | Limit the display to a **specific depth level** |
| `-a`         | Include **hidden files** (`.` prefix)           |
| `-d`         | Show **directories only**, no files             |
| `-f`         | Print the **full path** for each file/directory |


**Relative Path**

A relative path describes the location of a file or directory in relation to the current working directory.

Unlike an absolute path (which starts from the root /), a relative path is context-dependent — it changes depending on where you are.

#### 🧱 Special Path Symbols

| Symbol | Meaning                         |
| ------ | ------------------------------- |
| `.`    | Current directory               |
| `..`   | Parent directory (one level up) |
| `./`   | Current directory path prefix   |
| `../`  | Move up to the parent directory |


#### 🛣️ Absolute Path
An absolute path (or full path) specifies the exact location of a file or directory starting from the root directory (/), regardless of where you currently are.

It always begins with a / and does not depend on your current working directory.

| Command                          | Description                                              |
| -------------------------------- | -------------------------------------------------------- |
| `cd /home/ehbc`                  | Changes to the exact path from the root to `ehbc`'s home |
| `cat /home/ehbc/report.txt`      | Reads `report.txt` using the full path                   |
| `/home/ehbc/scripts/generate.sh` | Runs the script using the full path                      |

#### Relative vs Absolute

| Type     | Example                          | Description                           |
| -------- | -------------------------------- | ------------------------------------- |
| Absolute | `/home/ehbc/scripts/generate.sh` | Always the same, starts from root `/` |
| Relative | `scripts/generate.sh`            | Depends on where you run it from      |
